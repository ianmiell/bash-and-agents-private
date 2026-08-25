### General comments
- Shell as gatherer of context

  Go to compliance-framework/api and claude "find code related to networking in the api"
  eg
    sed -n '1,60p' internal/config/config.go | grep -n "allowedOrigins" | grep -n "allowedOrigins" -A5 -B5 internal/config/config.go | head -30

- "AI uses shell as its hands"

- AI uses shell and the command line to quickly inspect things, just like people do

- Shells allow AI to glue processes together

- Shells are very concise - fewer tokens!

