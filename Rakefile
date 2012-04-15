require 'rubygems'
require 'pony'
require 'yahoo_finance'

def send_mail(body, subject = 'finance report')
  Pony.mail({:to => ENV['TO_ADDRESS'],
             :subject => subject,
             :body => body,
             :via => :smtp,
             :via_options => {
               :address => 'smtp.sendgrid.net',
               :port => '587',
               :domain => 'heroku.com',
               :user_name => ENV['SENDGRID_USERNAME'],
               :password => ENV['SENDGRID_PASSWORD'],
               :authentication => :plain,
               :enable_starttls_auto => true}})
end

desc "Expetion value of SPDR500"
task "spy" do
  data = YahooFinance.quotes(["SPY", "USDJPY=X"], [:ask], {:raw => false})
  send_mail(data[0].ask * data[1].ask, 'Expection value of SPDR500')
end
