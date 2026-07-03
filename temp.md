Option 1: The Fast Way (Hardware Accelerated)
The Pi Zero 2 W has a built-in hardware video encoder (h264_omx). Using this offloads the work from the CPU to the GPU, making the conversion incredibly fast and keeping your CPU cool.


ffmpeg -i input.mkv -vf "scale=-2:240" -c:v h264_omx -b:v 500k -c:a aac -b:a 128k output.mp4
Note: Hardware encoders don't support CRF (Quality) targeting, so you must specify a bitrate instead (e.g., -b:v 500k, which is plenty for 240p).

Option 2: The High-Quality Way (CPU Bound)
If you want the absolute smallest file size with the best possible clarity, stick to the software encoder (libx264). However, you must use a faster preset, or the Pi's limited 512MB of RAM and CPU will cause it to crawl.


ffmpeg -i input.mkv -vf "scale=-2:240" -c:v libx264 -preset superfast -crf 24 -c:a aac -b:a 128k output.mp4
