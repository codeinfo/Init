PHP环境：

PHP: php5.2.5

Apache: apache2.2.13

 

1.下载ffmpeg－php：http://sergey89.ru/files/ffmpeg-php-win32-all.zip

2. 解压ffmpeg-php-win32-all.zip 后有下面几个文件：

     avcodec-51.dll

     avformat-51.dll

     avutil-49.dll

     php_ffmpeg.dll

     pthreadGC2.dll

 

3. 将四个文件拷贝到windows\system32文件夹下面（小插曲:之前自己再配置时候按照网上的文章只拷贝两个文件 avcodec-51.dll, avformat-51.dll到这个文件，结果发现并不能配置成功。后来将后面avutil-49.dll, pthreadGC2.dll全部拷贝过去就成功了，很有可能这四个文件是有一定关联使用的。）

     avcodec-51.dll, avformat-51.dll, avutil-49.dll, pthreadGC2.dll

 

4. 然后需要到apache\bin文件下找到php.ini文件下允许使用dll文件加入extension=php_ffmpeg.dll 并允许     extension=php_gd2.dll， extension=php_gettext.dll这两个
改动后如下（去掉前面的分号就代表允许执行）

    extension=php_gd2.dll
    extension=php_gettext.dll
    extension=php_ffmpeg.dll

 

5. 重新启动wamp后使用phpinfo()函数看到一下信息配置：
ffmpeg support (ffmpeg-php)	enabled
ffmpeg-php version 	0.5.2.1
libavcodec version 	Lavc51.43.0
libavformat version 	Lavf51.12.2
ffmpeg-php gd support 	enabled

 
Directive	Local Value	Master Value
ffmpeg.allow_persistent 	0 	0


 以上就表明ffmpeg在php环境中配置成功了。

 

6. 下面我们建立一个php的页面来测试是不是可以使用ffmpeg的一些函数功能。建立testvideo.php文件

 代码如下：

<?php

extension_loaded('ffmpeg');

$ffmpegInstance = new ffmpeg_movie('C:\wamp\www\top10.mp4');
echo "getDuration: " . $ffmpegInstance->getDuration()."<br>" .
"getFrameCount: " . $ffmpegInstance->getFrameCount()."<br>" .
"getFrameRate: " . $ffmpegInstance->getFrameRate()."<br>" .
"getFilename: " . $ffmpegInstance->getFilename()."<br>" .
"getComment: " . $ffmpegInstance->getComment()."<br>" .
"getTitle: " . $ffmpegInstance->getTitle()."<br>" .
"getAuthor: " . $ffmpegInstance->getAuthor()."<br>" .
"getCopyright: " . $ffmpegInstance->getCopyright()."<br>" .
"getArtist: " . $ffmpegInstance->getArtist()."<br>" .
"getGenre: " . $ffmpegInstance->getGenre()."<br>" .
"getTrackNumber: " . $ffmpegInstance->getTrackNumber()."<br>" .
"getYear: " . $ffmpegInstance->getYear()."<br>" .
"getFrameHeight: " . $ffmpegInstance->getFrameHeight()."<br>" .
"getFrameWidth: " . $ffmpegInstance->getFrameWidth()."<br>" .
"getPixelFormat: " . $ffmpegInstance->getPixelFormat()."<br>" .
"getBitRate: " . $ffmpegInstance->getBitRate()."<br>" .
"getVideoBitRate: " . $ffmpegInstance->getVideoBitRate()."<br>" .
"getAudioBitRate: " . $ffmpegInstance->getAudioBitRate()."<br>" .
"getAudioSampleRate: " . $ffmpegInstance->getAudioSampleRate()."<br>" .
"getVideoCodec: " . $ffmpegInstance->getVideoCodec()."<br>" .
"getAudioCodec: " . $ffmpegInstance->getAudioCodec()."<br>" .
"getAudioChannels: " . $ffmpegInstance->getAudioChannels()."<br>" .
"hasAudio: " . $ffmpegInstance->hasAudio();

 7.执行后如果拿到视频的一些信息如下就表示环境配置成功了，那我们就可以开始开发我们的视频转换了。

执行结果：

getDuration: 811.13336181641
getFrameCount: 12167
getFrameRate: 15
getFilename: C:\wamp\www\top10.mp4
getComment:
getTitle:
getAuthor:
getCopyright:
getArtist:
getGenre:
getTrackNumber: 0
getYear: 0
getFrameHeight: 240
getFrameWidth: 320
getPixelFormat: yuv420p
getBitRate: 269769
getVideoBitRate:
getAudioBitRate:
getAudioSampleRate: 48000
getVideoCodec: mpeg4
getAudioCodec: mpeg4aac
getAudioChannels: 2
hasAudio: 1