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

Note that this may require a C compiler as it may need to build cryptography dependancies.
You need to do this only once.

2. Generate a keypair.

You can also do this with openssl or many other tools.

~~~~
bundle exec ./keygen
~~~~

You should do this only one.
The private key is in signingkey.pem, and a self-signed certificate is in signingkey.crt.
A raw public key could be saved instead.

3. Sign some sbom data.

It loads the data from the file "sbom.dat", replace to suit.

~~~~
bundle exec ./signsbom
~~~~

Look at the results with cbor2pretty.rb, or cbor2diag.rb


4. Verify the result

It loads the data from sbom_signed.bin, which was produced in step 3.
If you didn't run step3, then you can use the reference file sbom\_signed-reference.bin.

~~~~
bundle exec ./verifysbom
~~~~

Please note that the "bundle exec" prefix is important as it sets up the Ruby include paths.


# Look inside

~~~~
%cbor2pretty.rb sbom_signed-reference.bin
d2                                      # tag(18)
   84                                   # array(4)
      43                                # bytes(3)
         a10126                         # "\xA1\x01&"
      a0                                # map(0)
      79 02a1                           # text(673)
         5350445856657273696f6e3a20535044582d322e320a446174614c6963656e73653a204343302d312e300a5350445849443a20535044585265662d444f43554d454e540a446f63756d656e744e616d653a20536f667477617265204173737572616e636520477561726469616e20506f696e74204d616e20285341472d504d290a446f63756d656e744e616d6573706163653a20646e733a736f6674776172656173737572616e6365677561726469616e2e636f6d0a43726561746f723a204f7267616e697a6174696f6e3a20646e733a72656c6961626c65656e65726779616e616c79746963732e636f6d0a43726561746f723a20546f6f6c3a205079496e7374616c6c657220332e360a437265617465643a20323032302d30392d30385431393a34343a31375a0a0a0a5061636b6167654e616d653a61696f646e730a5350445849443a20535044585265662d61696f646e732d322e302e300a5061636b616765537570706c6965723a20506572736f6e3a5361c3ba6c2049626172726120436f7272657467c3a90a5061636b61676556657273696f6e3a20322e302e300a5061636b616765436865636b73756d3a205348413235363a20616161356163353834663430666537373830313364663061613635343462663135373739396264336636303833363462343531383430656432633836383864650a5061636b616765446f776e6c6f61644c6f636174696f6e3a204e4f415353455254494f4e0a46696c6573416e616c797a65643a2066616c73650a5061636b6167654c6963656e73654465636c617265643a204e4f415353455254494f4e0a5061636b6167654c6963656e7365436f6e636c756465643a204e4f415353455254494f4e0a5061636b616765436f70797269676874546578743a204e4f415353455254494f4e0a0a # "SPDXVersion: SPDX-2.2\nDataLicense: CC0-1.0\nSPDXID: SPDXRef-DOCUMENT\nDocumentName: Software Assurance Guardian Point Man (SAG-PM)\nDocumentNamespace: dns:softwareassuranceguardian.com\nCreator: Organization: dns:reliableenergyanalytics.com\nCreator: Tool: PyInstaller 3.6\nCreated: 2020-09-08T19:44:17Z\n\n\nPackageName:aiodns\nSPDXID: SPDXRef-aiodns-2.0.0\nPackageSupplier: Person:Sa\xC3\xBAl Ibarra Corretg\xC3\xA9\nPackageVersion: 2.0.0\nPackageChecksum: SHA256: aaa5ac584f40fe778013df0aa6544bf157799bd3f608364b451840ed2c8688de\nPackageDownloadLocation: NOASSERTION\nFilesAnalyzed: false\nPackageLicenseDeclared: NOASSERTION\nPackageLicenseConcluded: NOASSERTION\nPackageCopyrightText: NOASSERTION\n\n"
      58 40                             # bytes(64)
         57d1bc5a66c8518e1fe8f6676f26af3d85611e75b4a8fb25dba6044b04185db1a87303f531d5c91ac479128eef2a15b1f99da17dc984177f37e794858824c7e8 # "W\xD1\xBCZf\xC8Q\x8E\x1F\xE8\xF6go&\xAF=\x85a\x1Eu\xB4\xA8\xFB%\xDB\xA6\x04K\x04\x18]\xB1\xA8s\x03\xF51\xD5\xC9\x1A\xC4y\x12\x8E\xEF*\x15\xB1\xF9\x9D\xA1}\xC9\x84\x17\x7F7\xE7\x94\x85\x88$\xC7\xE8"
~~~~
