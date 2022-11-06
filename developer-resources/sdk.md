---
description: A quick intro on how to setup the JustPush typescript SDK.
---

# Setting up SDK

### Installation and Set-Up

Start by creating a new project.

```shell
mkdir my-app
cd my-app
yarn init
npx tsc --init
```

{% hint style="info" %}
If you wish to use ES6 Modules syntax, then inside package.json set **“type” to “module”.**
{% endhint %}

Installation

```shell
# install the sdk and tronweb
yarn add @justpush/sdk tronweb
```

Usage&#x20;

```shell
mkdir src
touch src/index.ts 
```

<pre class="language-typescript"><code class="lang-typescript">const TronWeb = require('tronweb');
<strong>import { JustPush } from '@justpush/sdk';
</strong><strong>
</strong>const main = async () => {
    // Create a tronweb instance
<strong>    const tronWeb = new TronWeb({
</strong>        fullHost: 'https://api.trongrid.io',
        headers: { "TRON-PRO-API-KEY": 'your api key' },
        privateKey: 'your private key'
    });
    
    // Create a JustPush instance and pass the tronweb instance
    const justPush = new JustPush(tronWeb);
    
    // List subscribed groups
    const groups = (await justPush.listGroups({
        filter: {
            subscribed: true
        }
    })).groups;
    
    if (groups.length === 0) {
       return;
    }
    
    // list notification of the first group;
    const group = groups[0];      
    const notifications = (await justPush.listNotifications({
        groupId: group.id;
    })).notifications;
}
</code></pre>

If you are using the library on the frontend, you can retrieve the tronweb instance from tronlink extension as explained here.

{% embed url="https://developers.tron.network/v3.7/docs/tronlink-integration" %}
front-end
{% endembed %}

More documentation coming soon.&#x20;
