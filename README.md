 const express = require('express');
const fs = require('fs');
const bodyParser = require('body-parser');

const app = express();
const PORT = process.env.PORT || 3000;

app.use(bodyParser.json());

let receivedCommits = new Set();

app.post('/webhook', (req, res) => {
  const { repository, ref, commit, pushed_at } = req.body;

  if (!repository || !ref || !commit || !pushed_at) {
    return res.status(400).send('Invalid payload');
  }

  if (receivedCommits.has(commit)) {
    return res.status(200).send('Duplicate commit ignored');
  }

  receivedCommits.add(commit);

  const log = `Repo: ${repository}, Branch: ${ref}, Commit: ${commit}, Pushed At: ${pushed_at}\n`;
  fs.appendFileSync('webhook_log.txt', log);
  console.log(log);

  res.status(200).send('Webhook received');
});

app.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`);
});

