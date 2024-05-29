const express = require('express');
const bodyParser = require('body-parser');
const { conversation } = require('@assistant/conversation');

const app = express().use(bodyParser.json());
const port = process.env.PORT || 3000;

const appConv = conversation();

appConv.handle('Default Welcome Intent', conv => {
  conv.add('Hello, how can I assist you today?');
});

app.post('/fulfillment', appConv);

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
