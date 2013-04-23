!SLIDE smallest

# After 2.2 (Aggregation Framework) #

## Page views by region

    @@@ javascript
    db.events.ensureIndex({event: 1, "properties.Region": 1});

    db.events.aggregate(
        { $project: { _id: 0, event: 1, "properties.Region": 1 } },
        { $match: { event: "Viewed Product Page",
                    "properties.Region":{ $exists: true } } },
        { $group: { _id: "$properties.Region", count: { $sum:1 } } },
        { $sort: { count: -1 } },
        { $limit: 10 }
    );
