Calling [`transitionTo()`](http://emberjs.com/api/classes/Ember.Route.html#method_transitionTo) from a route or [`transitionToRoute()`](http://emberjs.com/api/classes/Ember.Controller.html#method_transitionToRoute) from a controller will stop any transition currently in progress and start a new one, functioning as a redirect. `transitionTo()` behaves exactly like the [link-to](../../templates/links) helper.

If the new route has dynamic segments, you need to pass either a *model* or an *identifier* for each segment. Passing a model will skip that segment's `model()` hook (since the model is already loaded).

## Transitioning Before the Model is Known

If you want to redirect from one route to another, you can do the transition in the [`beforeModel()`](http://emberjs.com/api/classes/Ember.Route.html#method_beforeModel) hook of your route handler.

```app/router.js Router.map(function() { this.route('posts'); });

    <br />```app/routes/index.js
    import Ember from 'ember';
    
    export default Ember.Route.extend({
      beforeModel() {
        this.transitionTo('posts');
      }
    });
    

If you need to examine some application state to figure out where to redirect, you might use a [service](../../applications/services).

## Transitioning After the Model is Known

If you need information about the current model in order to decide about redirection, you can use the [`afterModel()`](http://emberjs.com/api/classes/Ember.Route.html#method_afterModel) hook. It receives the resolved model as the first parameter and the transition as the second one. For example:

```app/router.js Router.map(function() { this.route('posts'); this.route('post', { path: '/post/:post_id' }); });

    <br />```app/routes/posts.js
    import Ember from 'ember';
    
    export default Ember.Route.extend({
      afterModel(model, transition) {
        if (model.get('length') === 1) {
          this.transitionTo('post', model.get('firstObject'));
        }
      }
    });
    

When transitioning to the `posts` route if it turns out that there is only one post, the current transition will be aborted in favor of redirecting to the `PostRoute` with the single post object being its model.

### Child Routes

Let's change the router above to use a nested route, like this:

```app/router.js Router.map(function() { this.route('posts', function() { this.route('post', { path: ':post_id' }); }); });

    <br />If we redirect to `posts.post` in the `afterModel` hook, `afterModel`
    essentially invalidates the current attempt to enter this route. So the `posts`
    route's `beforeModel`, `model`, and `afterModel` hooks will fire again within
    the new, redirected transition. This is inefficient, since they just fired
    before the redirect.
    
    Instead, we can use the [`redirect()`][5] method, which will leave the original
    transition validated, and not cause the parent route's hooks to fire again:
    
    [5]: http://emberjs.com/api/classes/Ember.Route.html#method_redirect
    
    ```app/routes/posts.js
    import Ember from 'ember';
    
    export default Ember.Route.extend({
      redirect(model, transition) {
        if (model.get('length') === 1) {
          this.transitionTo('posts.post', model.get('firstObject'));
        }
      }
    });