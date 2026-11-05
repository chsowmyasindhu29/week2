const express = require('express');
const app = express();
const PORT = 3000;

// Set EJS as the templating engine
app.set('view engine', 'ejs');

// Middleware to parse incoming URL-encoded form data (POST body)
app.use(express.urlencoded({ extended: true }));

// Initial array of user objects passed from the server
let users = [
    { name: "Rahul Sharma", email: "rahul@example.com", age: 21 },
    { name: "Priya Patel", email: "priya@example.com", age: 22 },
    { name: "Amit Verma", email: "amit@example.com", age: 20 }
];

// Part (a): GET route to render the users page with data
app.get('/users', (req, res) => {
    res.render('users', { userList: users });
});

// Part (b): POST route to accept and handle form data from the user
app.post('/add-user', (req, res) => {
    const { name, email, age } = req.body;
    
    // Add the new user data to the array
    if (name && email && age) {
        users.push({
            name: name,
            email: email,
            age: parseInt(age)
        });
    }
    
    // Redirect back to the users list page to display updated data
    res.redirect('/users');
});

// Start the server
app.listen(PORT, () => {
    console.log(Server is running at http://localhost:${PORT}/users);
});
