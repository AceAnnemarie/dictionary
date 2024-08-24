<script>
const express = require('express');
const { Pool } = require('pg');

const app = express();
const port = 3000;

// Replace these connection details with your actual PostgreSQL database information
const pool = new Pool({
  user: 'your_database_user',
  host: 'your_database_host',
  database: 'dictionary_db',
  password: '1062004',
  port: 5432,
});

app.use(express.json());

app.post('/api/insertWord', async (req, res) => {
  const { word, part_of_speech, definition, synonyms, antonyms, usage_example } = req.body;

  const query = `
    INSERT INTO words (word, part_of_speech, definition, synonyms, antonyms, usage_example)
    VALUES ($1, $2, $3, $4, $5, $6)
  `;

  try {
    await pool.query(query, [word, part_of_speech, definition, synonyms, antonyms, usage_example]);
    res.status(201).json({ message: 'Word inserted successfully' });
  } catch (error) {
    console.error('Error inserting word:', error);
    res.status(500).json({ error: 'Internal Server Error' });
  }
});

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});

</script>
