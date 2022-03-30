# How do I secure the remote modules?

Remote modules are simply JavaScript files. They have no more security exposure than split bundles, which
is a feature that has been available for years.

# I don't see state changes reflected between two different host applications

Module Federation shares code, not state. If you want components hosted on different pages to share state you need to use normal
state sharing mechanisms like REST or GraphQL API, or Websockets, or a servie like Firebase or Supabase.

# How does Module Federation handle routing?

Module Federation doesn't manage routes. Module Federation is just a mechanism to share code between applications.
What type of code you choose to share; components, routes, utility functions, i18n strings, is completely up to you.
But how you use that code in terms of routes, is completely up to you.

# Does Redux/Context/MobX/Valtio/Zustand/etc. work with Module Federation?

Yes, but, you will probably need to expose the store singleton from one application and consume it in your remote modules
in order to ensure that you are using the same global data store (or context).

# Doesn't a Monorepo do what Module Federation does?

No, a monorepo makes it easy to share code between applications at *build time*, where Module Federation makes it possible to
share code at runtime. If you have a component that is used in three different applications in a monorepo and you want to ensure that
a change to that component is deployed to all the applications you will need to redeploy all three applications from the monorepo.
With Module Federation and runtime dependencies you deploy the component once and it is consumed by all three applications at runtime
so the updating is instantaneous.

# Is Module Federation the only way to do Micro-Frontends?

No. A Micro-Frotend is just a self-contained component that manages its own state and connection to its Micro-services. You can
implement Micro-Frotends using npm modules hosted in different repositories, or in a single repository as a mono-repo, or using Module
Federation. Which mechanism you choose depends on your requirements.
