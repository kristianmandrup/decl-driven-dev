## Transport example

[MobX Websocket store](https://www.npmjs.com/package/mobx-websocket-store)

```js
import  MobxWebsocketStore from 'mobx-websocket-store';
import { autorun } from 'mobx';

const socket = ...
const store = new MobxWebsocketStore(
  (store) => {
    console.log("Opening websocket");
    socket = openSocket();
  },
  (store) => {
    console.log("Closing websocket");
    socket.close();
  },
  {
    id: 'MyStore',
    resetDataOnOpen: false
  }
);

autorun(() => {
  console.log(store.data);
});
```

### Firebase example

```js
import MobxWebsocketStore from 'mobx-websocket-store';
import firebase from "firebase";

firebase.initializeApp( ... );

const ref = firebase.database().ref("/messages");
const refListener = (snapshot: firebase.database.DataSnapshot) => {
  this.data = snapshot.val(); // 'this' will be bound later to the MobxWebsocketStore context
  this.atom.reportChanged();
};

const store = new MobxWebsocketStore(
  (store) => {
    console.log("Opening websocket");
    ref.on("value", refListener.bind(store));
  },
  (store) => {
    console.log("Closing websocket");
    ref.off("value", refListener.bind(store));
  }
);
```

`ChatRoom` component:

```js
@observer
class ChatRoom extends Component {
  render() {
    const messages = this.props.store.data;
    return (
      /* Render each message into a component */
    );
  }
}
```

And voila! Thanks to MobX atoms and a little MobX secret sauce, when a ChatRoom component is rendered, it will subscribe to the messages store, which will cause that store to start listening to that database reference. When the ChatRoom component stops being rendered, due to the user navigating elsewhere, the database reference will stop listening for changes.
