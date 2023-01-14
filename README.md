# fc-bus

A golang package for simplifying message bus communication in fc-hosting

## Requirements

A `kubemq` installation in the `kubemq` namespace of your cluster

## Usage

```go
// create context
ctx := context.Background()

// initialize bus
bus := events.Bus{
	Channel: "channel-name", // kubemq channel name
	ClientId: "test", // client id
	Context: ctx, // context
	TransportType: kubemq.TransportTypeGRPC, // set transport type
}

// connect to bus
// returns a kubemq.QueuesClient & an error
client, err := bus.Connect()

if err != nil {
	// ...
}

// register handler for messages on that queue
// returns a channel of type struct{} or an error
done, err := bus.Subscribe(client, func(msgs *kubemq.ReceiveQueueMessagesResponse, subscribeError error) {
	// process message
})
```
