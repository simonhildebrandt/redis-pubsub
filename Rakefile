require 'redis'

desc "Server"
task :server do
  redis = Redis.new

  loop do
    redis.publish 'channel9', Time.now.to_f
    sleep 0.1
  end
end

desc "Client"
task :client do

  threads = []

  threads << Thread.new do
     Redis.new.subscribe 'channel9' do |on|
      puts "subscribe"
      on.message do |channel, message|
        puts "Message 1: #{channel}, #{message}"
      end
    end
  end

  threads << Thread.new do
     Redis.new.subscribe 'channel9' do |on|
      puts "subscribe"
      on.message do |channel, message|
        puts "Message 2: #{channel}, #{message}"
      end
    end
  end

  threads.each { |thr| thr.join }

end
