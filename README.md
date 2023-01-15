# Bharat-News

Networking is an integral part of android development, especially when building data-driven clients. The java class mainly used for network connections is HttpUrlConnection. The class requires manual management of data parsing and asynchronous execution of requests. For network operations, we are better off using a library called Fast Android Networking Library which can take care of sending and parsing network requests. In this article, we will step through the process of building an android news application. Fast Android Networking Library supports all types of HTTP/HTTPS requests and in our app, we will use it for

Performing GET requests
Loading images from the internet into ImageViews
Here is what the application will look like in the end:

![Screenshot_20230115_171531](https://user-images.githubusercontent.com/106397517/212538861-69c1e0be-b368-4c9d-8538-447c8c13437f.jpg)
Step By Step Implementation
Step 1: Create a New Project 
To learn how to create a new project in Android Studio please refer to How to Create/Start a New Project in Android Studio/www.geeksforgeeks.com and choose java as the programming language.
Step 2: Add dependencies                                                                                                         

Select Gradle Scripts > build.gradle(Module:app) and add the below dependency in the dependencies section.
implementation 'com.amitshekhar.android:android-networking:1.0.2'
implementation 'com.amitshekhar.android:jackson-android-networking:1.0.2'

After adding the dependencies, sync your project by clicking Sync Now.

Step 3: Add permissions

Select manifests > AndroidManifest.xml and add the internet permission above the application tag.
<uses-permission android:name="android.permission.INTERNET" /> 

Step 4: Get an API Key  

Visit newsapi and register. The key will be displayed after registration and also sent to your email inbo

Step 5: Create a new empty activity and add a WebView to  the layout

Go to app > java > right-click > New > Activity > Empty Activity and name it as WebActivity. This activity will display web pages of articles as part of the activity layout.  To add a  WebView to the activity_web.xml file. Navigate to app > res > layout > activity_web.xml and add the below code to that file.
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:app="http://schemas.android.com/apk/res-auto"
	xmlns:tools="http://schemas.android.com/tools"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	tools:context=".WebActivity">

	<!-- webview to display web pages
		as part of the activity -->
	<WebView
		android:id="@+id/webview"
		android:layout_width="match_parent"
		android:layout_height="match_parent"/>

</LinearLayout>
Step 6: Working with the WebActivity.java file

Below is the code for WebActivity.java.

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.util.Log;
import android.webkit.WebView;

public class WebActivity extends AppCompatActivity {
	// setting the TAG for debugging purposes
	private static String TAG="WebActivity";

	// declaring the webview
	private WebView myWebView;

	// declaring the url string variable
	private String url;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_web);

		// assigning the views to id's
		myWebView = (WebView) findViewById(R.id.webview);

		Intent intent = getIntent();

		// checking if there is an intent
		if(intent!=null){
			// retrieving the url in the intent
			url = intent.getStringExtra("url_key");

			// loading and displaying a
			// web page in the activity
			myWebView.loadUrl(url);
		}

	}

	@Override
	protected void onRestart() {
		super.onRestart();
		finish();
	}
}
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.util.Log;
import android.webkit.WebView;

public class WebActivity extends AppCompatActivity {
	// setting the TAG for debugging purposes
	private static String TAG="WebActivity";

	// declaring the webview
	private WebView myWebView;

	// declaring the url string variable
	private String url;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_web);

		// assigning the views to id's
		myWebView = (WebView) findViewById(R.id.webview);

		Intent intent = getIntent();

		// checking if there is an intent
		if(intent!=null){
			// retrieving the url in the intent
			url = intent.getStringExtra("url_key");

			// loading and displaying a
			// web page in the activity
			myWebView.loadUrl(url);
		}

	}

	@Override
	protected void onRestart() {
		super.onRestart();
		finish();
	}
}
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.util.Log;
import android.webkit.WebView;

public class WebActivity extends AppCompatActivity {
	// setting the TAG for debugging purposes
	private static String TAG="WebActivity";

	// declaring the webview
	private WebView myWebView;

	// declaring the url string variable
	private String url;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_web);

		// assigning the views to id's
		myWebView = (WebView) findViewById(R.id.webview);

		Intent intent = getIntent();

		// checking if there is an intent
		if(intent!=null){
			// retrieving the url in the intent
			url = intent.getStringExtra("url_key");

			// loading and displaying a
			// web page in the activity
			myWebView.loadUrl(url);
		}

	}

	@Override
	protected void onRestart() {
		super.onRestart();
		finish();
	}
}
   
   
   
   import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.util.Log;
import android.webkit.WebView;

public class WebActivity extends AppCompatActivity {
	// setting the TAG for debugging purposes
	private static String TAG="WebActivity";

	// declaring the webview
	private WebView myWebView;

	// declaring the url string variable
	private String url;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_web);

		// assigning the views to id's
		myWebView = (WebView) findViewById(R.id.webview);

		Intent intent = getIntent();

		// checking if there is an intent
		if(intent!=null){
			// retrieving the url in the intent
			url = intent.getStringExtra("url_key");

			// loading and displaying a
			// web page in the activity
			myWebView.loadUrl(url);
		}

	}

	@Override
	protected void onRestart() {
		super.onRestart();
		finish();
	}
}

Step 7: Add a RecyclerView to the activity_main.xml file

Select app > res > layout > activity_main.xml and add the below code to that file. The  RecyclerView is used to efficiently display a list of data and in our case, it will display a list of news articles.

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:app="http://schemas.android.com/apk/res-auto"
	xmlns:tools="http://schemas.android.com/tools"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	tools:context=".MainActivity">

	<!-- A RecyclerView to efficiently
		display a list of articles -->
	<androidx.recyclerview.widget.RecyclerView
		android:id="@+id/recyclerview_id"
		android:layout_width="match_parent"
		android:layout_height="match_parent">
	</androidx.recyclerview.widget.RecyclerView>

	<!-- loading spinner to be displayed
		while the library fetches news -->
	<ProgressBar
		android:id="@+id/progressbar_id"
		android:layout_width="wrap_content"
		android:indeterminateTint="#0F9D58"
		android:layout_centerHorizontal="true"
		android:layout_centerVertical="true"
		android:layout_height="wrap_content">
	</ProgressBar>

</RelativeLayout>
Step 8: Create a new custom layout

Navigate to File > New > XML > Layout XML File and name it as article_item. The article_item.xml file will be used for each row within the news article list. Below is the code for the article_item.xml file.

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="match_parent"
	android:orientation="vertical"
	android:layout_height="wrap_content">

	<!-- horizontal LinearLayout containing
		image and article details -->
	<LinearLayout
		android:layout_width="match_parent"
		android:gravity="center"
		android:weightSum="10"
		android:orientation="horizontal"
		android:layout_height="wrap_content">

		<!-- Image of news thumbnail -->
		<!-- ANImageView is a view provided by
			Fast Android Networking Library -->
		<com.androidnetworking.widget.ANImageView
			android:id="@+id/image_id"
			android:layout_weight="3"
			android:layout_width="0dp"
			android:layout_height="wrap_content" />

		<LinearLayout
			android:layout_weight="7"
			android:layout_width="0dp"
			android:layout_height="wrap_content"
			android:padding="10dp"
			android:orientation="vertical">

			<!-- Text with title -->
			<TextView
				android:id="@+id/title_id"
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:ellipsize="end"
				android:maxLines="2"
				android:textStyle="bold"
				android:textColor="#0F9D58"
				android:textSize="14sp"/>

			<!-- Text with description name -->
			<TextView
				android:id="@+id/description_id"
				android:layout_marginTop="2dp"
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:ellipsize="end"
				android:fontFamily="sans-serif-medium"
				android:textAllCaps="false"
				android:textSize="12sp"/>

		</LinearLayout>

	</LinearLayout>

	<!-- Text with author name and date -->
	<TextView
		android:id="@+id/contributordate_id"
		android:layout_marginTop="1dp"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:ellipsize="end"
		android:maxLines="1"
		android:textSize="12sp" />

	<!-- View showing thin green horizontal
		line separating articles -->
	<View
		android:layout_width="match_parent"
		android:layout_marginTop="3dp"
		android:layout_marginBottom="5dp"
		android:layout_height="0.2dp"
		android:background="#0F9D58"/>

</LinearLayout>

Step 9: Create a NewsArticle Model class

Navigate to app > Java > package > Right Click on package> New > Java Class and name it as NewsArticle. We created this model class for storing news article data like title, content, description e.t.c.

In our model class, there are mainly three types of methods :  

Constructors: initializes newly created NewsArticle objects
Get methods: for getting property values
Set methods: for setting property values
Below is the code for the NewsArticle.java file.

public class NewsArticle {
	
	// the properties/attributes
	// of the ArticleModel
	String author;
	String title;
	String description;
	String url;
	String urlToImage;
	String publishedAt;
	String content;

	// ArticleModel empty constructor
	public NewsArticle() {
	}

	// get method : returns the name of the author
	public String getAuthor() {
		return author;
	}

	// set method : sets the author
	public void setAuthor(String author) {
		this.author = author;
	}

	// get method : returns the title of the article
	public String getTitle() {
		return title;
	}

	// set method : sets the title
	public void setTitle(String title) {
		this.title = title;
	}

	// get method : returns the description of the article
	public String getDescription() {
		return description;
	}

	// set method : sets the description
	public void setDescription(String description) {
		this.description = description;
	}

	// get method : returns url of the article
	public String getUrl() {
		return url;
	}

	// set method : sets the url of the article
	public void setUrl(String url) {
		this.url = url;
	}

	// get method : returns the urlToImage of the article
	public String getUrlToImage() {
		return urlToImage;
	}

	// set method : sets the UrlToImage
	public void setUrlToImage(String urlToImage) {
		this.urlToImage = urlToImage;
	}

	// get method : returns the date
	public String getPublishedAt() {
		return publishedAt;
	}

	// set method : sets the date
	public void setPublishedAt(String publishedAt) {
		this.publishedAt = publishedAt;
	}

	// get method : returns the content of the article
	public String getContent() {
		return content;
	}

	// set method : sets the title
	public void setContent(String content) {
		this.content = content;
	}
}

Step 10: Create an ArticleAdapter class  

Navigate to app > Java > package > Right Click on package> New > Java Class and name it as ArticleAdapter.
The ArticleAdapter class is responsible for getting data from the NewsArticle model and displaying it on view.
The adapter will provide access to the data items and is answerable for creating a view for each news article in the data set. 
Below is the code for the ArticleAdapter.java file.
import android.content.Context;
import android.content.Intent;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;
import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;
import com.androidnetworking.widget.ANImageView;
import java.util.ArrayList;

public class ArticleAdapter extends RecyclerView.Adapter<ArticleAdapter.ViewHolder> {
	// setting the TAG for debugging purposes
	private static String TAG="ArticleAdapter";

	private ArrayList<NewsArticle> mArrayList;
	private Context mContext;

	public ArticleAdapter(Context context,ArrayList<NewsArticle> list){
		// initializing the constructor
		this.mContext=context;
		this.mArrayList=list;
	}

	@NonNull
	@Override
	public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
		// inflating the layout with the article view (R.layout.article_item)
		View view=LayoutInflater.from(mContext).inflate(R.layout.article_item,parent,false);
		return new ViewHolder(view);
	}

	@Override
	public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
		// the parameter position is the index of the current article
		// getting the current article from the ArrayList using the position
		NewsArticle currentArticle=mArrayList.get(position);

		// setting the text of textViews
		holder.title.setText(currentArticle.getTitle());
		holder.description.setText(currentArticle.getDescription());

		// subString(0,10) trims the date to make it short
		holder.contributordate.setText(currentArticle.getAuthor()+
				" | "+currentArticle.getPublishedAt().substring(0,10));

		// Loading image from network into
		// Fast Android Networking View ANImageView
		holder.image.setDefaultImageResId(R.drawable.ic_launcher_background);
		holder.image.setErrorImageResId(R.drawable.ic_launcher_foreground);
		holder.image.setImageUrl(currentArticle.getUrlToImage());

		// setting the content Description on the Image
		holder.image.setContentDescription(currentArticle.getContent());

		// handling click event of the article
		holder.itemView.setOnClickListener(new View.OnClickListener() {
			@Override
			public void onClick(View view) {
				// an intent to the WebActivity that display web pages
				Intent intent = new Intent(mContext, WebActivity.class);
				intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
				intent.putExtra("url_key",currentArticle.getUrl());

				// starting an Activity to display the page of the article
				mContext.startActivity(intent);
			}
		});

	}

	@Override
	public int getItemCount() {
		return mArrayList.size();
	}

	public class ViewHolder extends RecyclerView.ViewHolder{

		// declaring the views
		private TextView title,description,contributordate;
		private ANImageView image;

		public ViewHolder(@NonNull View itemView) {
			super(itemView);
			// assigning views to their ids
			title=itemView.findViewById(R.id.title_id);
			description=itemView.findViewById(R.id.description_id);
			image=itemView.findViewById(R.id.image_id);
			contributordate=itemView.findViewById(R.id.contributordate_id);
		}
	}

}


Step 11: Working with the MainActivity.java file

In our activity, we will make GET requests to the news API using Android Fast Library and populate the RecyclerView with news articles. Firstly, 
we will create a string variable and set it to the API key (the key we created in step 4). 
For example if your API key = b971358de21d4af48ae24b5faf06bbok. 
Then declare the variable as :  

private static  String API_KEY="b971358de21d4af48ae24b5faf06bbok";
Below is the code for the MainActivity.java file.
import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.ProgressBar;
import com.androidnetworking.AndroidNetworking;
import com.androidnetworking.common.Priority;
import com.androidnetworking.error.ANError;
import com.androidnetworking.interfaces.JSONObjectRequestListener;
import com.jacksonandroidnetworking.JacksonParserFactory;
import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
	
	// TODO : set the API_KEY variable to your api key
	private static String API_KEY="";

	// setting the TAG for debugging purposes
	private static String TAG="MainActivity";

	// declaring the views
	private ProgressBar mProgressBar;
	private RecyclerView mRecyclerView;

	// declaring an ArrayList of articles
	private ArrayList<NewsArticle> mArticleList;

	private ArticleAdapter mArticleAdapter;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);

		// initializing the Fast Android Networking Library
		AndroidNetworking.initialize(getApplicationContext());

		// setting the JacksonParserFactory
		AndroidNetworking.setParserFactory(new JacksonParserFactory());

		// assigning views to their ids
		mProgressBar=(ProgressBar)findViewById(R.id.progressbar_id);
		mRecyclerView=(RecyclerView)findViewById(R.id.recyclerview_id);

		// setting the recyclerview layout manager
		mRecyclerView.setLayoutManager(new LinearLayoutManager(this));

		// initializing the ArrayList of articles
		mArticleList=new ArrayList<>();

		// calling get_news_from_api()
		get_news_from_api();
	}

	public void get_news_from_api(){
		// clearing the articles list before adding news ones
		mArticleList.clear();

		// Making a GET Request using Fast
		// Android Networking Library
		// the request returns a JSONObject containing
		// news articles from the news api
		// or it will return an error
		AndroidNetworking.get("https://newsapi.org/v2/top-headlines")
				.addQueryParameter("country", "in")
				.addQueryParameter("apiKey",API_KEY)
				.addHeaders("token", "1234")
				.setTag("test")
				.setPriority(Priority.LOW)
				.build()
				.getAsJSONObject(new JSONObjectRequestListener(){
					@Override
					public void onResponse(JSONObject response) {
						// disabling the progress bar
						mProgressBar.setVisibility(View.GONE);

						// handling the response
						try {

							// storing the response in a JSONArray
							JSONArray articles=response.getJSONArray("articles");

							// looping through all the articles
							// to access them individually
							for (int j=0;j<articles.length();j++)
							{
								// accessing each article object in the JSONArray
								JSONObject article=articles.getJSONObject(j);

								// initializing an empty ArticleModel
								NewsArticle currentArticle=new NewsArticle();

								// storing values of the article object properties
								String author=article.getString("author");
								String title=article.getString("title");
								String description=article.getString("description");
								String url=article.getString("url");
								String urlToImage=article.getString("urlToImage");
								String publishedAt=article.getString("publishedAt");
								String content=article.getString("content");

								// setting the values of the ArticleModel
								// using the set methods
								currentArticle.setAuthor(author);
								currentArticle.setTitle(title);
								currentArticle.setDescription(description);
								currentArticle.setUrl(url);
								currentArticle.setUrlToImage(urlToImage);
								currentArticle.setPublishedAt(publishedAt);
								currentArticle.setContent(content);

								// adding an article to the articles List
								mArticleList.add(currentArticle);
							}

							// setting the adapter
							mArticleAdapter=new ArticleAdapter(getApplicationContext(),mArticleList);
							mRecyclerView.setAdapter(mArticleAdapter);

						} catch (JSONException e) {
							e.printStackTrace();
							// logging the JSONException LogCat
							Log.d(TAG,"Error : "+e.getMessage());
						}

					}
					@Override
					public void onError(ANError error) {
						// logging the error detail and response to LogCat
						Log.d(TAG,"Error detail : "+error.getErrorDetail());
						Log.d(TAG,"Error response : "+error.getResponse());
					}
				});
	}
}




