<?php

class Image
{
    // 创建GIF动画
    function createGif($file_name, $words, $font_size = 28, $font_color = '#000000', $font_path, $bg = '#ffffff')
    {
        // 将十六进制颜色转换为RGB数组
        $bgColor = $this->hexToRgb($bg);
        $fontColor = $this->hexToRgb($font_color);

        // 获取字符串长度
        $length = mb_strlen($words, 'UTF-8');

        // 创建Imagick对象来存储GIF动画
        $gif = new Imagick();
        $gif->setFormat("gif");

        // 计算字符的边界框和文本宽度高度
        $bbox = imagettfbbox($font_size, 0, $font_path, $words);
        $text_width = $bbox[2] - $bbox[0];
        $text_height = $bbox[1] - $bbox[7];

        // 创建每一帧的图像
        for ($i = 0; $i < $length; $i++) {
            $curWord = mb_substr($words, 0, $i + 1, 'UTF-8');

            // 创建一个新图像以容纳当前文本
            $image = imagecreatetruecolor($text_width, $text_height);
            $bgColorAlloc = imagecolorallocate($image, $bgColor[0], $bgColor[1], $bgColor[2]);
            imagefill($image, 0, 0, $bgColorAlloc);

            // 绘制当前行的文本
            $fontColorAlloc = imagecolorallocate($image, $fontColor[0], $fontColor[1], $fontColor[2]);
            imagettftext($image, $font_size, 0, 0, $text_height, $fontColorAlloc, $font_path, $curWord);

            // 将GD图像转换为Imagick对象
            ob_start();
            imagegif($image);
            $frame_data = ob_get_contents();
            ob_end_clean();
            $frame = new Imagick();
            $frame->readImageBlob($frame_data);
            $frame->setImageDelay(10); // 设置每帧的延迟时间，单位是1/100秒
            $gif->addImage($frame);

            imagedestroy($image);
        }

        // 保存GIF动画
        $gif->writeImages($file_name, true);

        return $file_name;
    }

    // 创建精灵图
    private function createSprite($file_name, $words, $font_size=28, $words_color='#000000', $font_path, $bg='#ffffff')
    {
        // 将十六进制颜色转换为RGB数组
        $bgArr = $this->hexToRgb($bg);
        $wcArr = $this->hexToRgb($words_color);

        // 获取字符串长度
        $length = mb_strlen($words, 'UTF-8');

        // 计算单个字符的边界框
        $bbox = imagettfbbox($font_size, 0, $font_path, $words);
        $char_width = $bbox[2] - $bbox[0];
        $char_height = $bbox[1] - $bbox[7];

        // 计算图像的宽度和高度
        $image_width = $char_width * $length;
        $image_height = $char_height * $length;

        // 创建一个新图像以容纳所有行文本
        $image = imagecreatetruecolor($image_width, $image_height);

        // 设置背景色和字体颜色
        $bgColor = imagecolorallocate($image, $bgArr[0], $bgArr[1], $bgArr[2]);
        $color = imagecolorallocate($image, $wcArr[0], $wcArr[1], $wcArr[2]);

        // 填充背景色
        imagefill($image, 0, 0, $bgColor);

        // 绘制每一行文本
        for ($r = 0; $r < $length; $r++) {
            $curWord = mb_substr($words, 0, $r + 1, 'UTF-8');
            imagettftext($image, $font_size, 0, 0, ($r + 1) * $char_height, $color, $font_path, $curWord);
        }

        // 保存图像
        imagepng($image, $file_name);
        imagedestroy($image);

        return $file_name;
    }

    // 将十六进制颜色转换为RGB
    private function hexToRgb($hex)
    {
        // 去掉#号
        $hex = ltrim($hex, '#');

        // 如果是3个字符的简写形式，转换为6个字符的形式
        if (strlen($hex) == 3) {
            $hex = str_repeat($hex[0], 2) . str_repeat($hex[1], 2) . str_repeat($hex[2], 2);
        }

        // 将十六进制色值转换为十进制
        $r = hexdec(substr($hex, 0, 2));
        $g = hexdec(substr($hex, 2, 2));
        $b = hexdec(substr($hex, 4, 2));

        // 返回RGB数组
        return [$r, $g, $b];
    }

    // 将RGB颜色转换为十六进制
    private function rgbToHex($rgb)
    {
        $r = dechex($rgb[0]);
        $g = dechex($rgb[1]);
        $b = dechex($rgb[2]);

        // 保证每个颜色值是2个字符
        $r = strlen($r) == 1 ? '0' . $r : $r;
        $g = strlen($g) == 1 ? '0' . $g : $g;
        $b = strlen($b) == 1 ? '0' . $b : $b;

        return '#' . $r . $g . $b;
    }
}
