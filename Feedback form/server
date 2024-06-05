const express = require('express');
const bodyParser = require('body-parser');
const fs = require('fs');

const app = express();
const PORT = 3000;

app.use(bodyParser.json());
app.use(express.static('public'));

app.post('/submit-feedback', (req, res) => {
    const feedback = req.body;
    const feedbackData = `${new Date().toISOString()} - Name: ${feedback.name}, Email: ${feedback.email}, Feedback: ${feedback.feedback}\n`;
    
    fs.appendFile('feedback.txt', feedbackData, (err) => {
        if (err) {
            console.error('Error writing to file', err);
            res.status(500).json({ success: false });
        } else {
            res.json({ success: true });
        }
    });
});

app.get('/view-feedback', (req, res) => {
    fs.readFile('feedback.txt', 'utf8', (err, data) => {
        if (err) {
            console.error('Error reading file', err);
            res.status(500).send('Error reading feedback data');
        } else {
            res.send(`<pre>${data}</pre>`);
        }
    });
});

app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
