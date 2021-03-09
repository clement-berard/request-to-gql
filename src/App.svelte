<script>
    let curlInput;
    let resultQuery = '';
    let resultVariables = '';
    let hasBadFormat = false;

    function selectTextOnFocus(node) {

        const handleFocus = event => {
            node && typeof node.select === 'function' && node.select()
        }

        node.addEventListener('focus', handleFocus)

        return {
            destroy() {
                node.removeEventListener('focus', handleFocus)
            }
        }
    }

    function proceed() {
        hasBadFormat = false;
        if (curlInput) {
            try {
                const regex = /(--data-raw)(.)+/gm;
                const found = curlInput.match(regex)[0];
                const t1 = found.substring(12)
                const t2 = t1.slice(0, -3)
                const {variables, query} = JSON.parse(t2)
                console.log('query', query);
                console.log('variables', variables);
                resultQuery = query;
                resultVariables = JSON.stringify(variables, null, 2);
            } catch (e) {
                console.error('bad format');
                hasBadFormat = true;
            }
        }
    }
</script>

<main>

    <div>
        <h1 class="title is-1">Hello</h1>
        <div class="curl-entry">
            <textarea placeholder="curl" bind:value={curlInput} on:keyup={proceed}></textarea>
        </div>
        {#if hasBadFormat}
            <div class="notification is-danger">
                Bad format
            </div>
        {/if}
        <div class="results">
            <h3 class="title is-3">Result</h3>
            <div class="query">
                <textarea placeholder="query/mutation" use:selectTextOnFocus>{resultQuery}</textarea>
            </div>
            <div class="query">
                <textarea placeholder="variables" use:selectTextOnFocus>{resultVariables}</textarea>
            </div>
        </div>
    </div>
</main>

<style type="text/scss">
  main {
    text-align: center;
    padding: 1em;
    max-width: none;
    margin: 0 auto;

    textarea {
      width: 60vw;
      height: 400px;
    }
  }
</style>
