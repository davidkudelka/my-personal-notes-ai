  * schema.prisma consist of the 3 following parts
    * **Data sources** - specify the details of the data sources Prisma should connect to (e.g. a PostgreSQL database)
      * PostgreSQL, MySQL and SQLite are supported so far
      * You can see example in the prisma.schema file
    * **Generators** - Specifies what clients should be generated based on the data model (e.g. Prisma Client)
      * Currently the only client available is prisma-client-js
      * you can have different binaryTargets
      * You can use 
    * **Data model definition** - Specifies your application models (the shape of the data per data source) and their relations
      * Specifies your application models (the shape of the data per data source) and their relations
      * There are **Models**
        * Models have 2 major functions
          * Represent table in underlying database
          * Provide the foundation for the queries in the Prisma Client API
      * Getting a data model
        * Generating the data model from [[Prisma Introspection]] a database
        * Manually writing the data model and mapping it to the database with [[Prisma Migrate]]
  * **Auto formatting of the file**
    * Similar to other tools like gofmt and prettier, PSL syntax ships with a formatter for .prisma files. The formatter can be enabled in the VS Code extension
    * Extension is called Prisma
    * There is just one way to format the file, so unlike prettier, there is no settings
  * ## How to Access Your Database With Prisma Client
    * `npm install @prisma/client`
    * `prisma generate`
    * ```javascript
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

// Run inside `async` function
const allUsers = await prisma.user.findMany()```
  * ## Typical Prisma Workflows
    * ### SQL migrations and then [[Prisma Introspection]]
      * Manually adjust your database schema using SQL (maybe some other for migrations)
      * (Re-) introspect your database
      * Optionally (re-)configure your Prisma Client API
      * (Re-)generate Prisma Client
      * Use Prisma Client in your application code to access your database
        * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/Xymc54zzCI.png]]
    * ### Prisma Migrate
      * With [[Prisma Migrate]], the workflow looks slightly different
        * Manually adjust your Prisma data model
        * Migrate your database using the prisma migrate CLI commands
        * (Re-)generate Prisma Client
        * Use Prisma Client in your application code to access your database
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/31oMV1y_Ex.png]]