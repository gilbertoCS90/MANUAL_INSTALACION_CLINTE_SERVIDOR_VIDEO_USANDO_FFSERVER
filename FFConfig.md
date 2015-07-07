HTTPPort 8090
HTTPBindAddress 0.0.0.0
MaxHTTPConnections 2000
MaxClients 1000
MaxBandwidth 500000
CustomLog -                                 
UseDefaults

<Feed feed1.ffm>
    File /home/pruebas/Escritorio/tmp/feed1.ffm
    FileMaxSize 10000K
    ACL allow 172.10.71.78
        ACL allow 172.10.0.0 172.10.255.255
</Feed>
               
<Feed feed2.ffm>
    File /home/pruebas/Escritorio/tmp/feed2.ffm
    FileMaxSize 10000K
    ACL allow 172.10.71.78
        ACL allow 172.10.0.0 172.10.255.255
</Feed>


<Stream prueba.avi>
Feed feed1.ffm
Format avi
VideoFrameRate 15
VideoSize 352x240
VideoBitRate 256
VideoBufferSize 40
AudioBitRate 64
</Stream>

<Stream test.webm>
        Feed feed2.ffm
        Format webm
        AudioCodec vorbis
        AudioBitRate 32
        VideoCodec libvpx
        VideoSize 720x576
        VideoFrameRate 25
        AVOptionVideo flags +global_header
        AVOptionVideo cpu-used 0
        AVOptionVideo qmin 10
        AVOptionVideo qmax 42
        AVOptionVideo quality good
        AVOptionAudio flags +global_header
        StartSendOnKey
        VideoBitRate 128
        VideoBufferSize 256000
</Stream> 

<Stream status.html>
Format status
ACL allow 172.10.71.78
ACL allow 172.10.0.0 172.10.255.255
</Stream>

<Redirect index.html>
    URL http://www.ffmpeg.org/
</Redirect>
