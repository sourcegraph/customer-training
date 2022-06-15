I wanted to walk through what we'll cover in our instance config review meeting today. If you prefer, we do also offer an experimental `src validate` command in our CLI which will run through many of these same steps programatically—if you'd like, you can [review the documentation here](https://docs.sourcegraph.com/admin/validation). Otherwise, we can cover this manually on our call.

We'll want to look at:

1. Does a basic search work as we'd expect?
2. Does a non-main branch or tag search return results?
3. Have you configured the auth mechanisms that we discussed during scoping?
4. Are repo permissions enabled, if appropriate?
5. If we run a general search for `select:repo`, do we see the rough number of repos we'd expect?
6. Are all of the extensions we discussed during scoping enabled?

We'll also leave space for any other questions you might have, and schedule a kickoff training if we haven't already done so.

Thank you!
