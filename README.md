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
* `-rawcooked` - use RAWcooked rather than ffmpeg on its own to create FFV1/MKV
* `-short_test` - this will rawcooked 24 frames to a tmp directory, make a checksum manifest of the 24 frames, then unrRAWcooks/reversese the MKV, then make a checksum manifest of the unrawcooked DPX, and checks if the MD5s are identical. This seems to me to be a good trade-off between knowing that rawcooked will maintain your image data AND your metadata, and the time and space requried to do a full check.
* `-sip` - launches `sipcreator.py` to make a IFI-specific folder structure for the package.  
* `-i` - path to input DPX sequence
* `-o` - path to output 

This is not the final phase in our workflow, when this package has passed QC, we run an accessioning script which adds the accession number, a sha512 manifest, Digital Forensics XML (minus the hashes), descriptiove and technical metadata CSV and updates the log file.

It contains:  
* A checksum manifest
* logs/metadata/objects subfolders
* This log in particular contains a lot of information about the `seq2ffv1.py` process. Line 10 shows the losslessness verification judgement : https://github.com/kieranjol/rawcooked_examples/blob/master/ifi_rawcooked_sample_package/oe12345/87e25ab6-b666-4e2e-a993-60442d4c5556/logs/87e25ab6-b666-4e2e-a993-60442d4c5556_sip_log.log
* This log documents the ffmpeg framemd5 creation event: https://github.com/kieranjol/rawcooked_examples/blob/master/ifi_rawcooked_sample_package/oe12345/87e25ab6-b666-4e2e-a993-60442d4c5556/logs/87e25ab6-b666-4e2e-a993-60442d4c5556_source_framemd5.log
* This log documents the actual RAWcooked event via ffmpeg - https://github.com/kieranjol/rawcooked_examples/blob/master/ifi_rawcooked_sample_package/oe12345/87e25ab6-b666-4e2e-a993-60442d4c5556/logs/87e25ab6-b666-4e2e-a993-60442d4c5556_rawcooked.log
* This log documents the ffmpeg framemd5 creation event for the rawcooked MKV - https://github.com/kieranjol/rawcooked_examples/blob/master/ifi_rawcooked_sample_package/oe12345/87e25ab6-b666-4e2e-a993-60442d4c5556/logs/87e25ab6-b666-4e2e-a993-60442d4c5556_ffv1_framemd5.log
* The actual MKV file is in the `objects` subfolder
* in the metadata subfolder, there is mediainfo and mediatrace XML for the MKV file
* in the `supplemental` subfolder, there is Mediainfo, Mediatrace and Digital Forensics XML (minus the hashes) for the actual source DPX files.


