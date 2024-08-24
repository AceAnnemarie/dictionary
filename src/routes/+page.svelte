<script>
    let word = '';
    let partOfSpeech = '';
    let definition = '';
    let synonyms = '';
    let antonyms = '';
    let usageExample = '';
  
    async function addWord() {
      const response = await fetch('/api/words', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          word,
          part_of_speech: partOfSpeech,
          definition,
          synonyms: synonyms.split(',').map(s => s.trim()),
          antonyms: antonyms.split(',').map(a => a.trim()),
          usage_example: usageExample,
        }),
      });
  
      // Assuming the server responds with the newly added word
      const newWord = await response.json();
      console.log('New Word:', newWord);
  
      // You can update the todos array or trigger a refetch
    }
  </script>
  
  <h2>Add New Word</h2>
  
  <form on:submit|preventDefault={addWord}>
    <label>
      Word:
      <input bind:value={word} />
    </label>
  
    <label>
      Part of Speech:
      <input bind:value={partOfSpeech} />
    </label>
  
    <label>
      Definition:
      <textarea bind:value={definition}></textarea>
    </label>
  
    <label>
      Synonyms (comma-separated):
      <input bind:value={synonyms} />
    </label>
  
    <label>
      Antonyms (comma-separated):
      <input bind:value={antonyms} />
    </label>
  
    <label>
      Usage Example:
      <textarea bind:value={usageExample}></textarea>
    </label>
  
    <button type="submit">Add Word</button>
  </form>
  