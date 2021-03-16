# Software Bill of Materials (SBOM) signed with COSE

This code uses the ChariWT COSE library to sign a Software Bill of Materials.

0. Make sure you have a ruby interpreter

~~~~
apt install ruby bundler
~~~~

1. Install the dependancies

~~~~
bundle install
~~~~

2. Generate a keypair.

You can also do this with openssl or many other tools.

~~~~
bundle exec ./keygen
~~~~

3. Sign some sbom data.

It loads the data from the file "sbom.dat", replace to suit.

~~~~
bundle exec ./signsbom
~~~~

