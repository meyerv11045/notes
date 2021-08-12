# Software Engineering Notebook

### UML Class Diagram
- Visual diagram used to demonstrate classes, their attributes/functions, and the relationships between classes
- Useful to start one before a large project to see how all the components interact
- [Youtube Tutorial](https://www.youtube.com/watch?v=UI6lqHOVHic)
- [Lucid Chart](https://www.lucidchart.com/) (Online software used by numerous Fortune 500 companies for creating visual workspaces w/ things like UML diagrams)

### Class Construction
- Declare all fields as private/protected whenever possible
    - Use getter and setter functions to access and update class fields
- Initialize the fields in the constructor

## Code Readability
- Readability and maintainability separate coders from good coders
- Focus on being able to read and understand parts of parts of code (e.g. modules/functions) without having to read entire rest of codebase
- Code should be Intuitive and self-documenting
- Readability > Cleverness/Shortness
    - If you write the code as clever as possible, you will not be smart enough to debug it 
- Consistency in style (e.g. spacing, braces)

## Commenting/Documentation
- Learning to write good comments is a skill
- Any good developer can figure out *what* your code does so your comments should explain *why* it does it that way
    - Comment on why you made the decisions you did in your code

## Software Design Patterns
- Use encapsulation in order to separate concerns (i.e. possible points of breakdown in locally important assumptions such as object types) 
- Try to limit managing global states (e.g. updating/referencing) since that can easily get messy, complicated, and buggy
    - Clarity of a codebase greatly improves when pure functions that access no external state are used 
    - Functional languages like Haskell do this really well
- Don’t switch between programming designs (e.g. pub/sub, actors, MVC) in connected parts of a codebase
- Create Data Abstraction Layers
    - Ex: Don’t have queries for your database in your application code. Instead create a separate library between the database and application that handles all the queries and provides easy to use getter functions like load_users(). 
    - Creates consistent styles in queries
    - Limits the number of places to change queries if the DB schema changes

## Building a Software Stack
- Don’t reinvent the wheel when not necessary
- Reliance on 3rd-party/open source software does leave you vulnerable to their security issues and makes you reliant on other people’s maintenance of the dependencies 
- Choose Appropriate Database:
    - SQL: Postgres / MySQL / MariaDB / MemSQL / Amazon RDS
    - Key Value Stores: Redis / Memcache / Riak
    - NoSQL: MongoDB / Cassandra
    - Hosted DBs: AWS RDS / DynamoDB / AppEngine Datastore 
    - Heavy Lifting: Amazon MR / Hadoop (Hive/Pig) / Cloudera / Google Big Query

## Debugging
1. Come up w/ a hypothesis and test it (repeat until you fix the bug) 
   1. Think like a scientist when debugging 
   2. Record hypothesis and result
2. Reproduce the bug locally rather than on a server (if convenient) 
   1. Once you can fix it locally (which is faster & easier) you can change it on the server version
3. Read the source code carefully and make minor alterations according to your hypothesis
4. Use debuggers instead of messy print statements

## Problem Solving
1. Define the problem
2. Brainstorm (no idea is a bad idea)
3. Pseudo-Code (don’t worry about syntax- get the ideas down)
   1. Whiteboarding/writing is useful
4. Implement (test as you go and make sure each component works before moving on)
   1. Avoid building out a whole solution w/o testing any of the parts
5. Optimize efficiency (Go back and try to condense code, make more efficient, etc.)
   1. Time, memory, etc.
   2. Don't optimize too soon or overoptimize something that is fine
6. Transition solution to another language if learning a new language

## General Tips
- You are responsible for code quality
- Use meaningful names
- Write code that expresses intent
- Code should speak for itself (Less comments = Less maintenance)
- Leave the code better than you found it
- Single-responsibility code
- Function does one thing well
- Less arguments = better function
- Tests! (Test Driven Development)
- Work on the big picture skeleton for the program and then fill in the details later
- Interface first, implementation later
- Independent components that can be used in different places
- Master your craft
- Create a minimum viable product (MVP) with the base functionality and then iterate by adding more features

## Notes on SWE
- Not an industry, it’s a skill achieved with lots of practice
- Applicable to all industries available today (i.e. software runs everything)
- Solving problems is an art form-- you get better with lifelong practice

## Resources
1. [Readability & Software Design Practices](https://www.toptal.com/software/six-commandments-of-good-code)
2. [Clean Code (Book)](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
3. [Commenting Less](https://levelup.gitconnected.com/youre-commenting-your-code-too-much-and-other-controversial-thoughts-on-documentation-1ee617ed46af)
4. [REST API Design](https://medium.com/better-programming/restful-api-design-step-by-step-guide-2f2c9f9fcdbf)