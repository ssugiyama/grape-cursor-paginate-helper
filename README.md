# Grape::CursorPagineHelper

This library is Grape API Helper for [ActiveRecord::CursorPaginator](https://github.com/ssugiyama/active_record-cursor_paginator)

## Supported environment

- ActiveRecord
- Grape ( https://github.com/ruby-grape/grape )
- mysql or Postgresql

## Installation

Add the following line to your `Gemfile` and execute `bundle install`

```
gem 'grape-cursor_paginate_helper'
```

## Usage

Here is a typical api definition using Grape::CursorPaginateHelper

```ruby
class FakeAPI < Grape::API
  helpers Grape::CursorPaginateHelper
  resource :fake do
    desc 'cursor_paginate'
    cursor_paginate per_page: 10
    get '/cursor_paginate' do
      present cursor_paginate(Post.order(:display_index)).map(&:attributes).to_json
    end
  end
end
```

### parameters of CursorPaginator
- cursor: String - cursor to paginate
- per_page: Integer - record count per page (default to 10)
- direction: Symbol - direction to paginate. `:forward` (default) or `:backward`
- with_total: Boolean - if true, add total record count to headers as 'X-Total-Count'

### Items in Response Header

- `X-Previous-Cursor`: String - cursor of the first record. used for the backward paginate call.
- `X-Next-Cursor`: String - cursor of the last record. used for the forward paginate call.
- `X-Total`: Integer - total count of relation

## Development

### Run test

```shell
ADAPTER=mysql bundle exec rspec
ADAPTER=postgresql bundle exec rspec
```

## Contributing

Bug reports and pull requests are welcome on GitHub at . This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [code of conduct](https://github.com/ssugiyama/grape-cursor_paginate_helper/blob/main/CODE_OF_CONDUCT.md).

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Activerecord::CursorPagination project's codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/ssugiyama/grape-cursor_paginate_helper/blob/main/CODE_OF_CONDUCT.md).
