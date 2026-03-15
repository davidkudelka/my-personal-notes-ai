  * Tags:
    * [[GraphQL]]
  * Basic Info
    * Subscriptions depend on use of a publish and subscribe primitive to generate the events that notify a subscription. PubSub is a factory that creates event generators that is provided by all supported packages. PubSub is an implementation of the PubSubEngine interface, which has been adopted by a variety of additional [event-generating backends](https://www.apollographql.com/docs/apollo-server/data/subscriptions/#pubsub-implementations).
    * GraphQL subscription uses Web Sockets. Therefore Web Sockets must be supported
    * It supports authentication over web sockets
    * It supports filters, which helps with filtering of users which should be notified
    * It supports lifecycle events (onConnect, onDisconnect)
