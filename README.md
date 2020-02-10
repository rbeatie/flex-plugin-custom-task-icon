# Swapping Icons for TaskListItems

# TaskListItem
[https://media.twiliocdn.com/sdk/js/flex/releases/1.16.0/docs/TaskListItem.html](https://media.twiliocdn.com/sdk/js/flex/releases/1.16.0/docs/TaskListItem.html) 

`<TaskListItem {...TaskListItem.TaskListItemProps} />`

### TaskListItemChildrenProps

Properties of TaskListItem.
Properties:

|Name    |Type    |Attributes  | Description |
|:-------|:-------|:-----------|:-----------:|
|Badge|	Object    |	\<optional> | Set of properties for internal Badge element customisable by TaskChannel |

### TaskListItemProps

Properties of TaskListItem.

Properties:

|Name    |Type    |Attributes  | Description |
|:-------|:-------|:------|:-----------|
| visible|boolean| \<optional> | Whether the task list item is visible or not. |
| selected | boolean |\<optional> | Whether the task list item is selected or not.|
| selectedTaskSid |	string |\<optional> | Sid of the selected task.|
| onSelected |function |\<optional> |Callback when the task is selected.|
| **icon** | **string  React.ReactNode** | **\<optional>** | **Task list item icon.**|
| iconColor | string |	\<optional> |Icon color.|
| actions |	Array  <React.ReactElement.<any>> |\<optional>| Override default accept or reject actions.|
| firstLine |	React.ReactNode	| \<optional> |First line displayed in the task list item. |
| secondLine |	React.ReactNode	| \<optional> |Second line displayed in the task list item. |
| extraInfo |	React.ReactNode	| \<optional> |Additional info displayed in the task list item. |
| large |	boolean | \<optional> | Whether the item is large or not. If true, the lower area is displayed. |
| itemSize | TaskListItem.TaskListItemSize| \<optional> | Task list item size. |
| children | DynamicComponentChildren.<TaskListItem.TaskListItemChildrenProps> | \<optional> | children |


# Task Channel Definition API

## Defining A Voicemail Channel

### Where do I place the definition? 

You will may want to place this before the app initializes. Here we placed it inside of the plugins `init(flex, manager)` method. 
 
### Task Channel Definition

```jsx harmony

const definition = flex.DefaultTaskChannels.createDefaultTaskChannel(
      'voicemail',
      (task) => {
        console.log('Your almost there!', task);
        return task.taskChannelUniqueName === 'voicemail';
      }, "Hangup",
      "HangupBold",
      "#d2a926"
    );

flex.TaskChannels.register(definition);

```
### Icons

The icons used hewre are using is `Hangup` and `HangupBold`

[Flex Icons List](https://www.twilio.com/docs/flex/ui-icons)

# Notes

## Chat vs Call vs Default

These all behave differently. For example: 

>Call channel definition uses callbacks to determine the icon and colors (based on call state and destination to render)

Find more on the channel types here: [https://www.twilio.com/docs/flex/task-channel-definition-api#creating-custom-channel-definitions-with-helper-functions](https://www.twilio.com/docs/flex/task-channel-definition-api#creating-custom-channel-definitions-with-helper-functions)




























# Your custom Twilio Flex Plugin

Twilio Flex Plugins allow you to customize the appearance and behavior of [Twilio Flex](https://www.twilio.com/flex). If you want to learn more about the capabilities and how to use the API, check out our [Flex documentation](https://www.twilio.com/docs/flex).

## Setup

Make sure you have [Node.js](https://nodejs.org) as well as [`npm`](https://npmjs.com) installed.

Afterwards, install the dependencies by running `npm install`:

```bash
cd 

# If you use npm
npm install
```

## Development

In order to develop locally, you can use the Webpack Dev Server by running:

```bash
npm start
```

This will automatically start up the Webpack Dev Server and open the browser for you. Your app will run on `http://localhost:8080`. If you want to change that you can do this by setting the `PORT` environment variable:

```bash
PORT=3000 npm start
```

When you make changes to your code, the browser window will be automatically refreshed.

## Deploy

Once you are happy with your plugin, you have to bundle it in order to deploy it to Twilio Flex.

Run the following command to start the bundling:

```bash
npm run build
```

Afterwards, you'll find in your project a `build/` folder that contains a file with the name of your plugin project. For example, `plugin-example.js`. Take this file and upload it into the Assets part of your Twilio Runtime.

Note: Common packages like `React`, `ReactDOM`, `Redux` and `ReactRedux` are not bundled with the build because they are treated as external dependencies so the plugin will depend on Flex to provide them globally.