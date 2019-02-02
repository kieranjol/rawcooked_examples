# rawcooked_examples

Contents:
----------
DPX_48_frames:
-
 48 mandelbrot frames generated via:
` $ ffmpeg -report -f lavfi -i mandelbrot -pix_fmt gbrp10le -vframes 48 tests/dpx_48_frames/dont_call_me_eddie_%06d.dpx
`

ifi_sample_rawcooked_package
-
This contains a package that was created by this python script: https://github.com/kieranjol/IFIscripts/blob/master/seq2ffv1.py

The command line was :
`$ seq2ffv1.py -rawcooked -short_test -sip -i '/home/kieranjol/tests/dpx_48_frames' -o '/home/kieranjol/tests/output' `
These commands mean:
* `seq2ffv1.py` - calls the script
* `-i` - path to input DPX sequence
* `-o` - path to output 

This is not the final phase in our workflow, when this package has passed QC, we run an accessioning script which adds the accession number, a sha512 manifest, Digital Forensics XML (minus the hashes), descriptiove and technical metadata CSV and updates the log file.

It contains:  
* A checksum manifest
* logs/metadata/objects subfolders
* [This log in particular contains a lot of information about the `seq2ffv1.py` process](https://github.com/kieranjol/rawcooked_examples/blob/master/ifi_rawcooked_sample_package/oe12345/7fc037bd-c323-4db1-9b49-07c605ba6064/logs/7fc037bd-c323-4db1-9b49-07c605ba6064_sip_log.log). Line 15 shows the losslessness verification judgement which is generated via a comparison of the md5 checksums: 
* [This log documents the actual RAWcooked event via ffmpeg](https://github.com/kieranjol/rawcooked_examples/blob/master/ifi_rawcooked_sample_package/oe12345/7fc037bd-c323-4db1-9b49-07c605ba6064/logs/7fc037bd-c323-4db1-9b49-07c605ba6064.mkv_rawcooked.log)
* The actual MKV file is in the `objects` subfolder
* In the metadata subfolder, there is mediainfo and mediatrace XML for the MKV file and framemd5 manifests for the source DPX sequence and the MKV file
* In the `supplemental` subfolder, there is Mediainfo, Mediatrace and Digital Forensics XML (minus the hashes) for the source DPX files.

