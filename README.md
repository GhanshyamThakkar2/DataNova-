<h1>SQL to JSON Converter</h1>

<h2>📌 Overview</h2>
<p>This project converts <strong>SQL database schemas and data</strong> into structured <strong>JSON format</strong>. 
   It helps in migrating SQL-based data to NoSQL databases like MongoDB by parsing <code>CREATE TABLE</code>, 
   <code>INSERT INTO</code>, and <code>FOREIGN KEY</code> constraints.</p>

<h2>🚀 Features</h2>
<ul>
    <li>Parses <code>CREATE TABLE</code> statements to extract tables and columns.</li>
    <li>Detects <strong>foreign key relationships</strong> and converts them into JSON references.</li>
    <li>Processes <code>INSERT INTO</code> statements to generate JSON objects.</li>
    <li>Supports <strong>One-to-Many relationships</strong> using <code>$ref</code>.</li>
    <li>Outputs structured <strong>JSON ready for NoSQL databases</strong>.</li>
</ul>

<h2>📥 Example Input (SQL)</h2>
<pre>
CREATE TABLE Users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE
);

CREATE TABLE Orders (
    id INT PRIMARY KEY,
    user_id INT,
    product_name VARCHAR(255),
    FOREIGN KEY (user_id) REFERENCES Users(id)
);

INSERT INTO Users (id, name, email) VALUES (1, 'Alice', 'alice@example.com'), (2, 'Bob', 'bob@example.com');

INSERT INTO Orders (id, user_id, product_name) VALUES (1, 1, 'Laptop'), (2, 2, 'Phone');
</pre>

<h2>📤 Converted Output (JSON)</h2>
<pre>
{
    "Users": [
        { "id": 1, "name": "Alice", "email": "alice@example.com" },
        { "id": 2, "name": "Bob", "email": "bob@example.com" }
    ],
    "Orders": [
        { "id": 1, "user_id": { "$ref": "Users", "$id": 1 }, "product_name": "Laptop" },
        { "id": 2, "user_id": { "$ref": "Users", "$id": 2 }, "product_name": "Phone" }
    ]
}
</pre>

<h2>🔧 How It Works</h2>
<ol>
    <li>Provide your SQL schema and data as input.</li>
    <li>Run the converter, and it will parse tables, columns, and relationships.</li>
    <li>Get structured JSON output, ready for NoSQL databases or data processing.</li>
</ol>

<h2>📌 Why Use This?</h2>
<ul>
    <li>Easily migrate SQL databases to NoSQL formats like MongoDB.</li>
    <li>Automatically detect relationships and maintain references.</li>
    <li>No manual data transformation is required.</li>
</ul>
