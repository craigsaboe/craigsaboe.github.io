Title: Coding Standards Possibilities
Date: 2023-08-29 10:48:00
Modified: 2023-08-29 10:48:00
Category: 
Tags: 
Slug: 
Summary: 
Status: draft


1. Identifiers
	1. Auto Increment
	2. GUIDs
		1. Pros
			1. Prevent accidental mixups
				1. Accidentally run a delete against the wrong table? It won't find the record
				2. Accidentally insert into the wrong table? Foreign key violation
			2. Off-server generation
			3. Security - acts like a token and precludes certain attack vectors
		2. Cons
			1. Size
			2. Paging - randomness
			3. Less user-friendly - can't be remembered
	3. Natural Keys
		1. Can be tuples
		2. Do not be afraid to use!
		3. Pros
			1. Demonstrates intent
			2. No separate unique constraint
		4. Cons
			1. Size (when relating)
			2. Performance cost (based on size)
			3. Clunkiness in management
	4. [Friendly] "Names"
		1. Enumeration
		2. Examples: roles, locations
2. Databases
	1. Soft Deletes
		1. Should never be the default
		2. Break constraints/integrity
		3. Handle formally/explicitly never "automatically"
			1. Do not implement via CASCADE
		4. Approach:
			1. Graveyard
			2. Event sourcing
	2. Event Sourcing
		1. Log every transformation
		2. "Updated At" and "Updated By" not enough
	3. Constraints
		1. Start at data level
		2. In a perfect world, every representable state should be valid at the application level
			1. Allows distributed systems to function reliably without requiring perfect/consistent validation
		3. Split tables horizontally
			1. No mutually/dependently-non-nullable fields
				1. If you have 2+ fields that are either all null or all should have a value, split them out into another table with the same key as the original table and declare them non-nullable then join
		4. Encoding CHECK as COMPUTED in MySQL
	4. Lazy loading/iteration
		1. Don't fetch the entire result set
	5. Rarely [never] use DISTINCT
		1. Pretty much only has the possibility of hiding logical errors
	6. Rarely [never] use UNION (versus UNION ALL)
		1. Implicit DISTINCT
	7. Dynamic SQL
		1. Fixed strings only
	8. Parameterization
	9. Character encoding/collation
	10. Strict Mode
	11. MySQL Table Engine
		1. Default is dependent on version
		2. Never(?) use MyISAM
	12. Should we be considering Postgres?
		1. CHECK constraint support
		2. Timezone support
	13. ORDER BY
		1. Make sure combination of columns is unique, especially if using for pagination
		2. Order is non-deterministic in the absence of ORDER BY
3. Layers
	1. Data Access (ORM)
		1. Data de/serialization
	2. Logic/Business (Models/Entities)
		1. Assertions
		2. Relationships
		3. Actions/transformations/behaviors
	3. Control (Controllers)
		1. Input de/serialization
			1. Convert "stringly typed" (HTTP) into structured data
		2. Routing
		3. Authorization?
	4. Presentation (Templates)
		1. Display
		2. Input
4. Schedulers
	1. Data-driven versus Mutation/Impure
		1. Never structure a job assuming it runs reliably/on schedule
			1. Idempotence
5. Miscellaneous
	1. NO magic strings/number
		1. Define a constant
		2. Use an enumeration
	2. Limit mutable state
	3. Purity
		1. Prefer static classes/methods
			1. If a class doesn't encapsulate mutable state there's no reason to instantiate
			2. Generally nonsensical: $x = new X(); $x->x();
	4. Side effects are an implied portion of the return type
	5. Reduce [inappropriate] redundancy
		1. Focus on the semantics around the ability to vary independently - if two things should be bound together, figure out a way to bind them or maintainability suffers
	6. Timezones
		1. Always store and serve in UTC, format client side
		2. When comparing "day" make sure UTC is shifted to local
		3. Map to local client-side, and/or store a configuration application-side for the "application timezone"
	7. Centralize/abstract "base URL" if needed - don't concatenate explicitly at every URL callsite
		1. HTML base tag
		2. Extend jQuery.ajax or whatever library
	8. Boolean blindness
		1. Prefer constants/enumerations when appropriate
		2. Propagate evidence - value or null versus true or false
	9. Configuration
		1. Avoid hard-coding environment specific values
			1. Emails
			2. Domains/URLs
		2. Break up flags very granularly - prefer separate flags per feature rather than switching on, for example, "is production"
6. User Experience
	1. Never fail silently
7. Sending email
	1. Include headers to indicate that another automated system should not reply (prevent email loops/wars), and check for those headers on inbound emails before sending a reply
