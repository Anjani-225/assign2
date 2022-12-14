
# Full Stack Authenicated Payments System

The tech stack for the project ingestion

* Node.js
* Express.js
* JavaScript
* Postgres
* Reactjs

`scripts.sql` contains all the commands to be run in Postgres client
`src/router/AppRouter.js` contains all the routes and renders the components

## Authenication and Encryption ##
`mask.js` has code to display only the last 4 digist of your account number

generateAuthToken used to generate jwt token
Once the token is generated by generateAuthToken function, we insert that token along with the userid into the tokens table. So Whenever user logins, we generate a new token and add to the tokens table.
## Connections to Postgres ##
Postgresql database connection details in the connect.js

`async` function usage: If one of the connections fails then the other should not happen. 

If the transactions table is updated but the total_balance column value is not updated due to some error, then we need to revert the new data added in transactions table and vice versa. So we are executing these two things as a transaction therefore instead of pool.query, we are using client.query here where the statements that need to be executed together will be added in between await client.query('begin') and await client.query('commit'). If any of the queries in between these calls fail, we call await client.query('rollback') from inside catch block so the other transaction will be reverted means either both will succeed or none of them.

## To display transactions ##
`Generate Report` button on the summary page, we are calling the /transactions/account_id route by passing the selected start date and end date and get the list of transactions and add it to the redux store they are then send to `Report.js` to be displayed `downloadjs` is used to generate a pdf of the transactions
