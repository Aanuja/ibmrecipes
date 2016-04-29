## Building Chef Client 12.9.38

The Chef Client 12.9.38 code can be built for a Linux on z System running RHEL 7.1/6.6, SLES 12/11 & UBUNTU by following these instructions (Chef is available at https://www.chef.io/ and the github repository for the client can be found at https://github.com/chef/chef):

_**General Notes:**_   
_i) When following the steps below please use a standard permission user unless otherwise specified._  
_ii) A directory `/<source_root>/` will be referred to in these instructions, this is a temporary writable directory anywhere you'd like to place it._


## Building Chef Client on RHEL 7.1/6.6, SLES 12/11 & UBUNTU

1. Install the build dependencies

    For RHEL 7.1 
    ```
    TBD
    ```
	
    For RHEL 6.6 
    ```
    TBD  
    ```
    
    For SLES 11
    ```
    TBD	      
    ```

    For SLES 12
    ```
    TBD
    ```
	
	For UBUNTU
	```
    sudo apt-get install -y git ruby ruby-dev gcc make zlib1g zlib1g-dev libssl-dev libreadline-dev libgdbm-dev wget build-essential
    ```	
	    
2. For UBUNTU you will need Ruby 2.2.4
   
   ```
   cd /<source_root>/
   wget http://cache.ruby-lang.org/pub/ruby/ruby-2.2.4.tar.gz
   tar zxf ruby-2.2.4.tar.gz
   cd ruby-2.2.4
   ./configure
   make
   make test	  
   sudo make install
   ```
	
3. Move to the location you wish to store the Chef source in

    ```
    cd /<source_root>/
    ```

4. Clone the github Chef client repository checkout the correct version

    ```
    git clone https://github.com/chef/chef.git
    cd chef
    git checkout v12.9.38
    ```
	
5. Install the required version of the bundler ruby gem

   ```
   sudo gem install bundler
   ```
	
6. Use bundler to install Chef Client's ruby gem dependencies

   ```
   sudo bundle install
   ```
    
7. Build the Chef Client ruby gem packages

   ```
   bundle exec rake gem
   ```

8. Install the gem you just built

   ```
   ls pkg/*.gem | grep -v mingw32 | xargs sudo gem install
   ```    
   
9. Chef client is now built and installed (verify with chef-client or knife)


## Testing Chef Client

If you'd like to test the Chef client you've just built and installed, just follow the steps below:

1. Run the test suite
   	
   ```
   cd /<source_root>/chef/
   bundle exec rake spec
   ```  
   To run a single test file
   ```  
   bundle exec rspec spec/PATH/TO/FILE_spec.rb
   ```  
   To run a subset of tests
   ```
   bundle exec rspec spec/PATH/TO/DIR
   ```
   
   _**NOTE:** This may fail as there can be a dependency on rdoc/task in the Rakefile, if that happens just comment out the rdoc/task line as below._

   ```
   require "chef-config/package_task"
   require 'rdoc/task'
   require_relative 'tasks/rspec'
   ```
   can be changed to be

   ```
   require "chef-config/package_task"
   #require 'rdoc/task'
   require_relative 'tasks/rspec'
   ```
   
2. Visit https://github.com/chef/chef#testing for more   

## References:

https://github.com/chef/chef.git
