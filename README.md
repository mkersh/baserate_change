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
    * From a terminal:
    * (1.1) cd to a {ROOT-FOLDER} 
        * choose a filepath on your local machine for this {ROOT-FOLDER}
        * replace refs to {ROOT-FOLDER} below with this filepath
    *  (1.2) git clone https://github.com/mkersh/baserate_change.git
1. Add following aliases to your ~/.bash_profile (or equivalent):
    * (2.1) alias clojure-docker-baseratechange='cd {ROOT-FOLDER}/baserate_change;./rundocker-repl'
    * (2.2) alias clojure-docker-baserateREPL='cd {ROOT-FOLDER}/baserate_change;docker run -it -v $(pwd):/app -w /app mkersh65/clojure:version2 lein repl'
1. Edit your local src/http/ENV.clj file
    * ENV.clj contains details of the Mambu tenant to connect to and apiKey for authentication
        * setup "env17", which is the one the script is currently using
1. Edit your local [src/http/api/mambu/solutions/int_change/int_change.clj](https://github.com/mkersh/baserate_change/blob/main/src/http/api/mambu/solutions/int_change/int_change.clj)
    * <font size="1">Edit the PRODKEY_PREVIEW_MAP to container the variable-interest-rate product(s) and their corresponding calculator-product to use
        * Create the calculator-product by copying the product and changing the interest-rate-type to FIXED (leave all other settings the same).</font>
1. Goto {ROOT-FOLDER}/baserate_change folder in a terminal and run
    * Either the clojure-docker-baseratechange or clojure-docker-baserateREPL alias
        * Both start a clojure REPL in a docker container:
            * clojure-docker-baseratechange allows you to connect to the REPL from an Clojure editor/IDE
            * clojure-docker-baserateREPL runs a simple REPL in the docker container
1. clojure-docker-baserateREPL - Once the REPL has started copy and run either [1] or [2] below:
    * ;; [1] Get a single account update, for a baserate-change=0.5% on 2022-09-01
    * (get-single-loan-schedule-update "2022-09-01" 0.5 "VMPL903")
    * ;; [2] Get updates for all variable-rate loans accounts, , for a baserate-change=0.5% on 2022-09-01
    * (get-loan-schedule-updates-after-baserate-change "2022-09-01" 0.5)




