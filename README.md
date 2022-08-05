# baserate_change

See [src/http/api/mambu/solutions/int_change/int_change.clj](https://github.com/mkersh/baserate_change/blob/main/src/http/api/mambu/solutions/int_change/int_change.clj) for the main script.

Provides an implementation of "Approach-5: Using getPreviewLoanAccountSchedule to see interest-rate change" in Clojure.


## Running code - From a docker container

Using docker is the safest way to run this script from a work computer.

Pre-requisite(s):
1. Docker
1. Git
1. Code Editor - Like MS VSCode


Instructions:
1. Clone https://github.com/mkersh/baserate_change.git onto your machine
    1. cd to a $ROOT-FOLDER 
        * choose a filepath on your local machine for this $ROOT-FOLDER and replace with this in all references to $ROOT-FOLDER below
    1. git clone https://github.com/mkersh/baserate_change.git
1. Add following aliases to your ~/.bash_profile (or equivalent):
    1. alias clojure-docker-baseratechange='cd $ROOT-FOLDER/baserate_change;./rundocker-repl'
    1. alias clojure-docker-baserateREPL='cd $ROOT-FOLDER /baserate_change;docker run -it -v $(pwd):/app -w /app mkersh65/clojure:version2 lein repl'
1. Edit your local src/http/ENV.clj file
    1. This contains details on the Mambu tenant to connect to and apiKey for authentication
        1. setup env for "env17", which is the one the script is using
1. Edit your local [src/http/api/mambu/solutions/int_change/int_change.clj](https://github.com/mkersh/baserate_change/blob/main/src/http/api/mambu/solutions/int_change/int_change.clj)
    * Edit the PRODKEY_PREVIEW_MAP to container the variable-interest-rate product(s) and their corresponding calculator-product to use
        * Create the calculator-product by copying the product and changing the interest-rate-type to FIXED - Leave all other settings the ssame
1. Goto {{root-folder}}/baserate_change folder in a terminal and run
    1. One of the aliases above, either clojure-docker-baseratechange or clojure-docker-baserateREPL
        1. Both start a clojure REPL in a docker container:
            1. clojure-docker-baseratechange allows you to connect to the REPL from an Clojure editor/IDE
            1. clojure-docker-baserateREPL runs a simple REPL in the docker container
1. clojure-docker-baserateREPL - Once the REPL has started type:
    * (load "http/api/mambu/solutions/int_change/int_change")
    * (in-ns 'http.api.mambu.solutions.int_change.int_change)
    * 
    * ;; Then choose one of the two options below:
    * ;; Get a single account update
    * (get-single-loan-schedule-update "2022-09-01" 0.5 "VMPL903")
    * ;; Get updatess for all variable-rate loans accounts
    * (get-loan-schedule-updates-after-baserate-change "2022-09-01" 0.5)




