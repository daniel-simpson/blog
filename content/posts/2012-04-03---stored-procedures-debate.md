---
title: The Stored Procedures Debate
date: "2012-04-03"
template: "post"
draft: false
slug: "/posts/2012/stored-procedures-debate/"

tags:
- "sql"
- "stored-procedures"
- "rant"
description: "Having just started a new job where I'll be working on a particular product for some time, I've spent the last couple of days reviewing the code base, documentation and database structure."
---
Having just started a new job where I'll be working on a particular product for some time, I've spent the last couple of days reviewing the code base, documentation and database structure.

In my last role I was tasked with porting a website from the Ektron CMS to ASP.NET MVC 4.  The CMS database consisted of hundreds of tables, views, stored procedures and table-valued functions.

The database that I designed for the website ended up being no more than twenty tables, two views, one scalar-valued function and one stored procedure (which was only used for resetting data and hence did not make it into the production database).

The database running the system I am now tasked to work with has evolved over time, and has its quirks but on the whole it's fairly solid and stable.  The lead developer on the team is of the mindset that everything must run through stored procedures, a point of view that I do not share.

I will not say that stored procedures are not necessary, however I will repeat the phrase used quite frequently when it comes to this discussion - "The right tool for the right job."

Stored procedures have their place, they are efficient and can be useful, however creating a stored procedure to perform single insert, update, delete and select in my opinion is overkill.

The following two calls will perform essentially the same.  Obviously where «InsertIntoMyTable» is essentially a wrapper for the insert statement.

    INSERT INTO [MyTable] ( [Column1], [Column2], [Column3] ) VALUES ( @Value1, @Value2, @Value3 )
     
    -- or
     
    EXEC InsertIntoMyTable @Value1, @Value2, @Value3

The question you need to ask yourself is whether you are willing to commit to maintaining the stored procedures as your model evolves.

If you are writing a stored procedure that deletes a lot of data, copies a lot of data, or anything that involves batching, I say go ahead.  If you're just inserting or updating single records, stored procedures are not the tool for your job.