---
title: Twilio SMS in Ruby
author: PipisCrew
date: 2016-02-12
categories: [news]
toc: true
---

[http://twilioinc.wpengine.com/2016/02/how-to-send-twilio-sms-in-ruby-in-5-minutes.html](http://twilioinc.wpengine.com/2016/02/how-to-send-twilio-sms-in-ruby-in-5-minutes.html)

```js
require 'sinatra'
require 'twilio-ruby'

post '/receive_sms' do
  content_type 'text/xml'

  response = Twilio::TwiML::Response.new do |r|
    r.Message 'Hey thanks for messaging me!'
  end

  response.to_xml
end

post '/send_sms' do
  # Phone number to send to
  to = params["to"]
  # Message to send
  message = params["body"]

  client = Twilio::REST::Client.new(
    ENV["TWILIO_ACCOUNT_SID"],
    ENV["TWILIO_AUTH_TOKEN"]
  )

  client.messages.create(
    to: to,
    from: "+12155844169",
    body: message
  )
end
```

origin - http://www.pipiscrew.com/?p=3742 twilio-sms-in-ruby