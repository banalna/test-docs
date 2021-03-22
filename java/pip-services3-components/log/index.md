

# [Command](#)

Concrete implementation of [ICommand](#ICommand) interface. Command allows to call a method or function using Command pattern.

```typescript
var command = new Command("add", null, async(args) => {
var param1 = args.GetAsFloat("param1");
var param2 = args.GetAsFloat("param2");
return param1 + param2; });
var result = command.ExecuteAsync("123", Parameters.fromTuples(
"param1", 2,
"param2", 2 ));
Console.WriteLine(result.ToString()); 
// Console output: 4
```

See [ICommand](#ICommand), [CommandSet](#CommandSet)


# [CommandSet](#)
Contains a set of commands and events supported by a [commandable](#ICommandable) object. The CommandSet supports command interceptors to extend and the command call chain.

CommandSets can be used as alternative commandable interface to a business object. It can be used to auto generate multiple external services for the business object without writing much code.

See [Command](#Command), [Event](#Event), [ICommandable](#ICommandable)

### Example
```typescript
export class MyDataCommandSet extends CommandSet {
    private _controller: IMyDataController;

    constructor(controller: IMyDataController) { // Any data controller interface
        super();
        this._controller = controller;
        this.addCommand(this.makeGetMyDataCommand());
    }

    private makeGetMyDataCommand(): ICommand {
        return new Command(
          'get_mydata',
          null,
          (correlationId: string, args: Parameters, callback: (err: any, result: any) => void) => {
              let param = args.getAsString('param');
              this._controller.getMyData(correlationId, param, callback);
          }
        );
    }
}
```

# [Event](#)

Concrete implementation of [IEvent](#IEvent) interface. It allows to send asynchronous notifications to multiple subscribed listeners.
See [IEvent](#IEvent), [IEventListener](#IEventListener)

### Example
```typescript
let event = new Event("my_event");

event.addListener(myListener);

event.notify("123", Parameters.fromTuples(
  "param1", "ABC",
  "param2", 123
));
```

# [ICommand](#)


# [ICommandable](#)


# [ICommandIntercepter](#)


# [IEvent](#)


# [IEventListener](#)


# [InterceptedCommand](#)