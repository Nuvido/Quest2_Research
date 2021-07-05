# BMBF

## ANDROID MANIFEST

## CODE

### BMBF.dll
BMBF.dll contains the Main activity, logging tools, feed config

#### Main Activity
Main activity first begins with importing varies system and custom libaries. The application then begins to create a web view instance, and then checks whether it has write permissions. 


```
protected override void OnCreate(Bundle savedInstanceState)
		{
			Platform.Init(this, savedInstanceState);
			this.SetContentView(2131427356);
			base.OnCreate(savedInstanceState);
			this._webView = base.FindViewById<WebView>(2131230925);
			this._browserView = base.FindViewById<WebView>(2131230926);
			this._toastInjector = new ToastInjectorWebViewClient(this._browserView);
			this._browserView.SetWebViewClient(this._toastInjector);
			WebSettings settings = this._browserView.Settings;
			string text = "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2049.0 Safari/537.36 BMBF_Quest/";
			Version version = Assembly.GetExecutingAssembly().GetName().Version;
			settings.UserAgentString = text + ((version != null) ? version.ToString() : null);
			this._browserView.SetWebChromeClient(new WebChromeClient());
			this._browserView.Settings.JavaScriptEnabled = true;
			this._browserView.Settings.AllowContentAccess = true;
			this._browserView.Settings.CacheMode = -1;
			this._browserView.Focusable = true;
			this._browserView.Settings.MediaPlaybackRequiresUserGesture = false;
			this._browserView.Settings.DomStorageEnabled = true;
			this._browserView.Settings.DatabaseEnabled = true;
			this._browserView.Settings.DatabasePath = "/data/data/" + this._browserView.Context.PackageName + "/databases/";
			this._browserView.Download += new EventHandler<DownloadEventArgs>(this._webView_Download);
			this._toastInjector.Download += new EventHandler<string>(this._toastInjector_Download);
			this._webViewClient = new BMBFWebViewClient(this, this._webView);
			this._webViewClient.JSInterface.OnBrowserGoBack += new EventHandler(this.JSInterface_OnBrowserGoBack);
			this._webViewClient.JSInterface.OnHideBrowser += new EventHandler(this.JSInterface_OnHideBrowser);
			this._webViewClient.JSInterface.OnNavigateBrowser += new EventHandler<string>(this.JSInterface_OnNavigateBrowser);
			this._webViewClient.JSInterface.OnRefreshBrowser += new EventHandler(this.JSInterface_OnRefreshBrowser);
			this._webViewClient.JSInterface.OnShowBrowser += new EventHandler<int>(this.JSInterface_OnShowBrowser);
			this._webViewClient.JSInterface.OnToast += new EventHandler<JSInterface.ToastMsg>(this.JSInterface_OnToast);
			WebSettings settings2 = this._webView.Settings;
			string userAgentString = settings2.UserAgentString;
			string text2 = " BMBF_Quest/";
			Version version2 = Assembly.GetExecutingAssembly().GetName().Version;
			settings2.UserAgentString = userAgentString + text2 + ((version2 != null) ? version2.ToString() : null);
			if (this.CheckSelfPermission("android.permission.WRITE_EXTERNAL_STORAGE") != null)
			{
				ActivityCompat.RequestPermissions(this, new string[]
				{
					"android.permission.WRITE_EXTERNAL_STORAGE"
				}, 1);
			}
		}
```
