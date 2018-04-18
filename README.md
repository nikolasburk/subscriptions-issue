# Subscriptions

Reproduce the issue:

1. Clone the repo
2. Deploy prisma service
3. Start `publications` subscription on app layer
4. Start `post` subscription on database layer
5. Send `writePost` mutation on app layer
6. The subscription is triggered on the database layer, not on the app layer

If you remove the `where` argument in the `publications` subscription in `index.js`, the subscription also fires on the app layer:

```js
subscribe: async (parent, args, ctx, info) => {
  return ctx.db.subscription.post(
    {
      // where: {
      //   mutation_in: ['CREATED', 'UPDATED'],
      // },
    },
    info,
  )
```
