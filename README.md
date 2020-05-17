# CC
# THIS IS NOT SUPPORTED BY MICROSOFT

for Communication Compliance

Powershell command sample

ログイン情報を $UserCredential に割り当てます。
$UserCredential = Get-Credential 

次にSession変数を指定します。
$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://ps.compliance.protection.outlook.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection 

以下のコマンドによって、このモジュールで使われるコマンドをローカルコンピュータではなくてSessionターゲットに対して実行します。
Import-PSSession $Session -DisableNameChecking 

Xmlファイルをアップロードします。XMLは、Unicodeで保存するのを忘れずに。
New-DlpSensitiveInformationTypeRulePackage -FileData (Get-Content -Path "C:\<filepath>\filename.xml" -Encoding Byte) 


IDごと確認
Get-DlpSensitiveInformationType -Identity "Regex" 

Xmlの削除 
Remove-DlpSensitiveInformationTypeRulePackage -Identity "3490e580-f35a-4031-9ca0-3683959b87ca" 

ログの取得 
Get-SupervisoryReviewPolicyReport | select Policy, ItemCount 

切断 
Remove-PSSession $Session 

ーーーーーーーーーーーー
From Docs.microsoft.com
XMLの作り方
https://docs.microsoft.com/ja-jp/microsoft-365/compliance/create-a-custom-sensitive-information-type-in-scc-powershell?view=o365-worldwide

アップロード方法
https://docs.microsoft.com/ja-jp/powershell/module/exchange/policy-and-compliance-dlp/new-dlpsensitiveinformationtyperulepackage?view=exchange-ps
