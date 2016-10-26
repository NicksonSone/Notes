# Procedure to Deploy New Technology:

Never dive into details first. Estimate the usability: 
clustering support, 
functionality,
backup support, 
features, 
what's better than original solution,
solutions of other company, 
richnes of online resource(how vibrate the community is)

# For database:
connector(performance, availability of resources)
cache, 
read/write performance, 
transaction, 
clustering, 
sharding(partitioning), 
ease of upgrade backup


# Http Delete Method

HTTP regulation suggest do not pass parameters in DELETE method.


# Model Relation

After model design phase, some models must have some kind of relations to each other. Updates
of one record could have unexpected impact on related data in other model. This influence must
be taken into consideration.


# Functionality Conflicts 

two versions of api for the same functionality can have substantial impact on data model. If the 
newer interface perform differently on data, data conflicts and contradicting diplaying rule may 
occur. This is a very special case for two devices using different sets of api


# Software Implementation Scheduling

Scheduling should be based on complexity of implementation and related functions, including 
interaction between database and client side. Data in database usually support creatiion, update,
query and delete on client side or operation system. Conflicts in data race ought to be fully 
examined and considered

$ \sum_{\forall i}{x_i^{2}} $
