<script lang="ts">
  type task = {
    title: string;
    description: string;
  };
  let tasks: task[] = [];
  let inputTitle: string = "";
  let inputDescription: string = "";
  $: inputtedTitle = inputTitle.length === 0;
  const add = (): void => {
    tasks = [
      ...tasks,
      {
        title: inputTitle,
        description: inputDescription,
      } as task,
    ];
  };
  const remove = (index: number): void => {
    tasks = tasks.filter((_, i: number) => {
      return i !== index;
    });
  };
</script>

<ol>
  {#each tasks as t, i (i)}
    <li>
      タイトル: {t.title}
      <br />
      詳細: {t.description}
      <br />
      <button on:click={() => remove(i)}>削除</button>
    </li>
  {/each}
</ol>

<input type="text" bind:value={inputTitle} placeholder="タイトル" />
<br />
<textarea bind:value={inputDescription} placeholder="詳細" />
<br />
<button on:click={add} disabled={inputtedTitle}>追加</button>

<style>
  button {
    font-family: inherit;
    font-size: inherit;
    padding: 1em 2em;
    color: #ff3e00;
    background-color: rgba(255, 62, 0, 0.1);
    border-radius: 2em;
    border: 2px solid rgba(255, 62, 0, 0);
    outline: none;
    width: 200px;
    font-variant-numeric: tabular-nums;
    cursor: pointer;
  }

  button:focus {
    border: 2px solid #ff3e00;
  }

  button:active {
    background-color: rgba(255, 62, 0, 0.2);
  }
  button:disabled {
    color: #cbb0a7;
    background-color: rgba(212, 157, 138, 0.1);
  }
</style>
