import mysql from 'mysql';

// Create a connection pool
const pool = mysql.createPool({
  host: 'your-database-host',
  user: 'your-database-user',
  password: 'your-database-password',
  database: 'your-database-name',
});

export default async (req, res) => {
  try {
    // Get a connection from the pool
    const connection = await pool.getConnection();

    // Perform database query or operation
    const results = await connection.query('SELECT * FROM your_table');

    // Release the connection back to the pool
    connection.release();

    // Send the results as response
    res.status(200).json(results);
  } catch (error) {
    res.status(500).json({ error: 'Database error' });
  }
};
