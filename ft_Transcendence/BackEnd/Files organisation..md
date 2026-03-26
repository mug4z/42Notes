## Files
Quick description of the different folder and file for the backend.
- Docker: contain the dockerfile used by the dockercompose to build the backend.
- prisma: contain all the prisma configuration files (schema and config) and migrations.
	- schema.prisma : represent how the database is build.
	- `*config.ts` : represent the different options for prisma.
- src: All the source files to be transpiled to javascript.
- test: All the test for the backend.
- Makefile : for now this is present to init the database with prisma.
- package.json: all the package needed for the backend.
- tsconfig.json : the different configuration for transpiled typescript to javascript.


Organisation from "high-level" to "low-level"
1. Routes
2. Schemas
3. Controllers
4. Models