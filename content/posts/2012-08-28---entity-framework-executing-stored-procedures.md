---
title: Entity Framework executing stored procedures
date: "2012-08-28"
template: "post"
draft: false
slug: "/posts/2012/entity-framework-executing-stored-procedures/"

tags:
- "development"
- "c-sharp"
- "entity-framework"
- ".net"
description: "Let's start with the code..."
---
Let's start with the code...

    public IEnumerable<T> ExecuteStoredProcedure<T>(string name, object parameters)
    {
        if (parameters != null)
        {
            var _parameters = parameters.GetType().GetProperties().Select(x => new SqlParameter()
            {
                ParameterName = x.Name,
                Value = x.GetValue(parameters, null)
            }).ToArray();
                
            var sql = name + " " + string.Join(", ", _parameters.Select(p => "@" + p.ParameterName));
                
            return Database.SqlQuery<T>(sql, _parameters);
        }
        else
        {
            return Database.SqlQuery<T>(name);
        }
    }

... and finish with an explanation.

We needed a way to execute stored procedures and deal with the data returned from them.  The code above will take the name of a stored procedure and execute it against the database returning a strongly typed enumerable of entities.

This method lives within my context class that derives from `DbContext` but can be used anywhere you can access `DbContext.Database`.

Obviously there's plenty of flaws with it, but I literally just wrote it and decided to share.  Feel free to discuss issues in the comments...