


##	定义适配器

````java

public class MyFragmentPagerAdaptert extends FragmentPagerAdapter {

	private List<Fragment> fragments;
	private FragmentManager fm;
	
	public MyFragmentPagerAdaptert(FragmentManager fm,
			ArrayList<Fragment> fragments) {
		super(fm);
		this.fragments = fragments;
		// TODO Auto-generated constructor stub
	}

 

	/*
	 * 获取组元素
	 * @see android.support.v4.app.FragmentPagerAdapter#getItem(int)
	 */
	@Override
	public Fragment getItem(int position) {
		// TODO Auto-generated method stub
		return fragments.get(position);
	}

	@Override
	public int getCount() {
		return fragments.size();
	}
	public void setFragments(ArrayList<Fragment> fragments) {
		if (this.fragments != null) {
			FragmentTransaction ft = fm.beginTransaction();
			for (Fragment f : this.fragments) {
				ft.remove(f);
			}
			ft.commit();
			ft = null;
			fm.executePendingTransactions();
		}
		this.fragments = fragments;
		notifyDataSetChanged();
	}
//	@Override
//	public Object instantiateItem(ViewGroup container, final int position) {
//		Object obj = super.instantiateItem(container, position);
//		return obj;
//	}
}

````


##	2：定义fragment

````java
public class MyFragment extends Fragment {

	Activity activity;
	String tag;
	public MyFragment(String tag) {
		super();
		this.tag = tag;
	}
	@Override
	public void onCreate(Bundle savedInstanceState) {
		// TODO Auto-generated method stub
		Bundle args = getArguments();
		 
		super.onCreate(savedInstanceState);
	}
	@Override
	public void onAttach(Activity activity) {
		// TODO Auto-generated method stub
		this.activity = activity;
		super.onAttach(activity);
	}
	@Override
	public View onCreateView(LayoutInflater inflater, ViewGroup container,
			Bundle savedInstanceState) {
		// TODO Auto-generated method stub
		 View view = LayoutInflater.from(getActivity()).inflate(R.layout.fragment1, null);
		 TextView textview1 = (TextView) view.findViewById(R.id.textView1);
		 
		 textview1.setText(tag);
		 
		 return view;
	}
}

````


##	3:页面使用

````java

private void initFragment() {
		 ArrayList<Fragment> fragments = new ArrayList<Fragment>();
		 Fragment fragment1 = new MyFragment("fragment1");
		 Fragment fragment2 = new MyFragment("fragment2");
		 Fragment fragment3 = new MyFragment("fragment3");
		 fragments.add(fragment1);
		 fragments.add(fragment2);
		 fragments.add(fragment3);
		MyFragmentPagerAdaptert adapter = 
				new MyFragmentPagerAdaptert(getSupportFragmentManager(),fragments);
		viewPager = (ViewPager) findViewById(R.id.viewPager);
		viewPager.setAdapter(adapter);
 
	}
````