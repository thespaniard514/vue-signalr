# vue-signalr

Forked from https://github.com/latelierco/vue-signalr

My updates were to the listeners. You can now send as many params in the signature from the server and the package will use js spreading to pass them along to the socket listener function.

```
Example Server:

public async Task SendMessage(string user, string message)
{
    await Clients.All.SendAsync("ReceiveMessage", user, message);
}
```
```
Example Client:

sockets: {
    ReceiveMessage(user, message) {
      console.log(user, message);
    },
  },
```

## Get started


```js
import Vue from 'vue'
import VueSignalR from 'vue-signalr'

Vue.use(VueSignalR, 'SOCKET_URL');

new Vue({
  el: '#app',
  render: h => h(App),
  
  created() {
    this.$socket.start({
      log: false // Active only in development for debugging.
    });
  },

});
```

## Example with component

```js
Vue.extend({

  ...
  
  methods: {
  
    someMethod() {
      this.$socket.invoke('socketName', payloadData)
        .then(response => {
          ...
        })
    }
    
    async someAsyncMethod() {
      const response = await this.$socket.invoke('socketName', payloadData)
      ...
    }
    
  },

  // Register your listener here. 
  sockets: {
  
    // Equivalent of
    // signalrHubConnection.on('someEvent', (data) => this.someActionWithData(data))
    someEvent(data) {
      this.someActionWithData(data)
    }
    
    otherSomeEvent(data) {
      this.otheSomeActionWithOtherSomeData(data)
    }
    
  }

});


```
