
design decision i came up with

renamed the injuries controller to the posts controller since i wanted to base the controller off an actual model and thought that that design decision may be a little confusing

I originally had it that way becuase i wanted my routes to be named /injuries , /injuries/new  etc but realized I can pass an option to my resources like this : resources :posts, only: [:index, :new, :show], path: 'injuries'

AWESOME.