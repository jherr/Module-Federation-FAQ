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

# Can I use a mono-repo in conjunction with Module Federation?

Absolutely. You can share the same component both dynamically using Module Federation and as build-time dependency as a fallback using a 
mono-repo.

# How does Module Federation relate to SingleSPA?

SingleSPA is a system that makes it easy to host components written in different frontend frameworks on the same page. For example a React application
can host an Angular component packaged as a SingleSPA parcel. SingleSPA can use Module Federation to load the component parcels. So these two
technologies can be used together. Module Federation does **not** have any mechanism that allows you to run code from one view framework within a
different view framework. Though it will happily allow you to import that code.

# How do I share CSS using Module Federation?

You can only share JavaScript code with Module Federation. You can't share CSS as CSS, or images as images. One approach to styling Micro-Frontends
is to use a shared stylesheet between the host applications, and to use a CSS-in-JS solution, like emotion, to refine the styles of the
components.

# How does TypeScript work with Module Federation?

Module Federation shares JavaScript files at runtime. When the TypeScript files are compiled and deployed the types are gone.
One recommendation for using type with Module Federation is to use shared "contract" libraries that define the types of exposed modules.
And these contract libraries should be used by both host and remote to ensure that shared code conforms to those contracts.
