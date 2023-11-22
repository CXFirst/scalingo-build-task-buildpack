# Scalingo buildpack task runner

Run a rake task during the [Scalingo](https://scalingo.com) image build to modify your docker image (i.e. download fonts, move things around, ...)

# Installation

Within your project create a `build` task that can be called with `bundle exec rake 'build:build' `

```ruby
# lib/tasks/build.rake

namespace :build do
  desc "Build hook"
  task :build do |_t, args|
    # your logic here
    # do not forget that during build time the root project path will not be `/app/app` but something like `/build/<uuid>/app/...`
    # thus you need to use `Rails.root.join('app', ...)`
  end
end
```

Add a `.buildpacks` at the root of your project with all the needed [buildpacks](https://doc.scalingo.com/platform/deployment/buildpacks/intro) and the current one

For example :
```
# .buildpacks

https://github.com/Scalingo/apt-buildpack.git
https://github.com/Scalingo/nodejs-buildpack.git
https://github.com/Scalingo/ruby-buildpack.git
https://github.com/CXFirst/scalingo-build-task-buildpack.git
```

Finally deploy on Scalingo
