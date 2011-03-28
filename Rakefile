require 'pony'

EMAIL_FROM  = 'server@example.com'
EMAIL_TO    = 'me@example.com'

def handle_exception(exception)
  $stderr.puts "#{name} aborted!"
  $stderr.puts exception.message
  $stderr.puts exception.backtrace.join("\n")

  # Send email

  subject = "Rake exception - #{exception.message}"
  body = "#{exception.message}\n\n#{exception.backtrace.join("\n")}"
  
  Pony.mail(:to => EMAIL_TO, :from => EMAIL_FROM, :subject => subject, :body => body)
  
  $stderr.puts
  $stderr.puts
  $stderr.puts "Exception details sent to #{EMAIL_TO}"
end

module Rake

  class Application
 

    def standard_exception_handling
      begin
        yield
      rescue Exception => e
        handle_exception(e)
        exit(false)
      end
      
    end

  end
  
end

# Include this to run 'rake test:foo'
# load 'test.rake'
