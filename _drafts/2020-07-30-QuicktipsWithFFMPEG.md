ffmpeg -y -i input1.mp4 -c copy -bsf:v h264_mp4toannexb -f mpegts temp1 2> /dev/null & ffmpeg -y -i input2.mp4 -c copy -bsf:v h264_mp4toannexb -f mpegts temp2 2> /dev/null & ffmpeg -f mpegts -i "concat:temp1|temp2" -c copy -bsf:a aac_adtstoasc output.mp4


file week05-part1.mp4
file week05-part2.mp4
file week05-part3.mp4



# removed chapters
-map_chapters -1


# concatenate files
ffmpeg -f concat -safe 0 -i stream.txt -c copy CaseStudyWeek02.mp4



# compress a file
 ffmpeg -i input.mp4 -vcodec libx265 -crf 28 output.mp4


# if you get a stream/packet size error add this before the output statement
-max_muxing_queue_size 1024
