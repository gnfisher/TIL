# User `stale?` to leverage HTTP caching

We can speed up our more expensive endpoints by using [`stale?`](https://api.rubyonrails.org/classes/ActionController/ConditionalGet.html#method-i-stale-3F), a method that will check certain HTTP headers and only render a response when the client's cached content is out of date.

The `stale?` method works by setting the etag and last-modified HTTP headers and comparing them to the etag sent with the client request.
If the client's request doesn't match the etag generated, the client's request is considered stale and a new response is generated.
If the client's request does match, the controller will respond with a `304 Not Modified` status and skips the rendering step altogether.

```ruby
def show
  @article = Article.find(params[:id])

  if stale?(etag: @article, last_modified: @article.updated_at)
    @statistics = @article.really_expensive_call
    respond_to do |format|
      # all the supported formats
    end
  end
end
```

The `stale?` method can work with a few other headers and options [including `If-Modified-Since`](https://thoughtbot.com/blog/take-control-of-your-http-caching-in-rails), too.

