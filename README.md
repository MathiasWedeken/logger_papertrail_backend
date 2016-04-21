# LoggerPapertrailBackend

A [Papertrail](https://papertrailapp.com) backend for [Elixir Logger](http://elixir-lang.org/docs/stable/logger/Logger.html).

[Change Log](CHANGELOG.md)


## Installation

Available in [Hex](https://hex.pm/packages/logger_papertrail_backend). The package can be installed as:

  1. Add `logger_papertrail_backend` to your list of dependencies in `mix.exs`:

        def deps do
          [{:logger_papertrail_backend, "~> 0.1.0"}]
        end

  2. Ensure `logger_papertrail_backend` is started before your application:

        def application do
          [applications: [:logger_papertrail_backend]]
        end

  3. In your `config.exs` (or in your `#{Mix.env}.exs`-files):

        config :logger, :logger_papertrail_backend,
          host: "logs.papertrailapp.com:<port>",
          level: :warn,
          system_name: "Wizard",
          format: "$metadata $message"

        # alternatively use :url for shorter config
        # prepend with "papertrail://" or "syslog://"
        # then host:port/system_name

        config :logger, :logger_papertrail_backend,
          url: "papertrail://logs.papertrailapp.com:<port>/<system_name>",
          level: :warn,
          format: "$metadata $message"

        config :logger,
          backends: [ :console,
            LoggerPapertrailBackend.Logger
          ],
          level: :debug

    * (Required) Follow "Add System" in your Papetrail dashboard to get `:host` values
    * (Optional) Set `:level` for this backend (overides global `:logger`-setting )
    * (Optional) Set specific `:system_name` in Papertrail, defaults to current application-name
    * (Optional) Set :format, defaults to `[$level] $levelpad$metadata $message`, see [Logger.Formatter](http://elixir-lang.org/docs/stable/logger/Logger.Formatter.html)
    * Other supported options in config are `:colors`, `:metadata`. See :console-docs in [Elixir.Logger](http://elixir-lang.org/docs/stable/logger/Logger.html)




## Example output:

`Oct 02 14:19:04 Wizard UpptecSlack.SlackBot:  [info]   Successfully authenticated as user "wizard" on team "Upptec"`


Papertrail sets timestamp when message arrives. `Wizard` is `:system_name`. `UpptecSlack.SlackBot` is the module sending the log. `[Info]` is level.
