
# Order move through question

#### GAIN CONTEXT ON THE PROBLEM
1. spawn agents to explore the codebase, and to explain component and important services
2. How will this new feature/ticket integrate with the system
3. Use your context to guide the AI into specific parts of the codebase, to not waste context

> Example: Lets say you are giving a issue where you have a gRPC service that generates reports, however the reports generated have now become long running tasks, that causes client side request timeouts

When exploring the system, you can guide it based on that info:
- Check the entry point of the gRPC function that generates reports. explain how it is used, what the function does, and the output. 
- Give an example workflow of this usage, starting from the client calling the function, to the gRPC function actually does, to what it responds with. As you go through the high level steps, flag anything that might potentially cause time outs or long running processes.
- What might be causing issues, is it running synchronously on a single thread or async. Investigate and give suggestions



#### Generate requirement docs / Engineering doc
1. For bigger systems
	1. Functional and non functional
	2. artechicaul flow is pretty important, all the moving pieces
	3. high level, So focus on maybe important data entities, and how they communicate together. Also some access patterns and diagrams
	4. and some low level design, So maybe interface definitions, API endpoints, ect.
2. For smaller tickets and OOP questions
	1. Pieces involved +  data entities
	2. implementation plan