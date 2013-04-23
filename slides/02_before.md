!SLIDE smallest

# Before 2.2 (MapReduce) #

## Page views by region

    @@@ javascript
    db.events.ensureIndex({event: 1});

    var map = function() {
        if (this.properties.Region) {
          emit(this.properties.Region, 1);
        };
    };

    var reduce = function(key, values) {
        return values.reduce(function(a,b) { return a + b; }, 0);
    };

    db.events.mapReduce(map, reduce, 
        { 
            out: { inline: true },
            query: { event: "Viewed Product Page" }
        }
    );
