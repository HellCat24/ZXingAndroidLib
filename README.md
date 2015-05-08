ZXingAndroidLib is basic Zxing lib implementation.

To implement this lib you need to:
- clone this project
- import it to your current project
- add it as dependency in gradle
    - in setting.gradle add 
    `"include 'your_path:ZXingAndroidLib:app'"`
    - in build.gradle add it to dependency
    ```
    dependencies {
    ...
    
    compile project('your_path:ZXingAndroidLib:app'')
    ```
}
- to genarate QR Code
  - in Intent specify Contents.Type you want to use and data - string to encoude
  ```
    Intent intent = new Intent(Intents.Encode.ACTION);
    intent.putExtra(Intents.Encode.TYPE, Contents.Type.TEXT);
    intent.putExtra(Intents.Encode.DATA, data);`
  ```
  - create QRCodeEncoder qrCodeEncoder = new QRCodeEncoder(getActivity(), intent);
  - use requestQRCode to generate QRCode
  ```
            qrCodeEncoder.requestQRCode(data, 150, new QRCodeEncoder.OnCompleteListener() {
            @Override
            public void onComplete(Bitmap qrCodeView) {
                
            }

            @Override
            public void onFail() {
               
            }
        });
  ```
  - to scan QR Code
    - `startActivityForResult(new Intent(getActivity(), CaptureActivity.class), YOUR_REQUEST_CODE);`
    - result will be delivered in 
    ```
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        if (resultCode == Activity.RESULT_OK) {
            switch (requestCode) {
                case YOUR_REQUEST_CODE:
                    String result = data.getStringExtra(Intents.Scan.RESULT);
                    break;
            }
        }
    }
    ```
