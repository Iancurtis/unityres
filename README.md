# unityres
resource manager for unity slua 

## ��ʼ��

### res.initialize(wwwlimit, editormode, abpath2assetinfo, errorlog)

* wwwlimit ʵ���˶�WWW����Դ���ޡ�Ҫ>=1����ζ��ͬʱ����������WWW��
	
	* windows�ϲ��Խ��Ϊ��������1000��WWW�����ܻ�����200�����ҵ��̣߳������editormode������10000������ʾtoo many thread����

* editormode �������true����ʹ��ͬ������AssetDatabase.LoadAssetAtPath 

* abpath2assetinfo ��assetinfo.csvֱ�����ɡ����������������assetbundleʱ����cache������assetbundle��

* errorlog ����Ϊ(message), ���Ϊnil���ڻ����lua��error


### res.load_manifest(assetinfo, callback)

* �������λ��cache�У���Ҫһ�����أ���Զ�����ڴ���

* �����editormode������Ҫ�����������

* assetinfo ��ʽΪ { assetpath: xx, abpath: xx, type: xx, location: xx, cache: xx }��

	* ��assetinfo.csv�ж�ȡ����assetinfo.csv�ɴ���������ɡ�assetinfo.csv��assetpath��Ϊprimary key������typeΪasetbundleʱassetpath==abpath��

	* type ����Ϊ { assetbundle = 1, asset = 2, prefab = 3 }�� location ����Ϊ { www = 1, resources = 2 }��

	* cache ΪCache���һ��instance������ʵ����lru��

* callback ����Ϊ (err, asset) 

	* errΪnilʱ��asset��Ϊnil������ɹ�

	* err��Ϊnilʱ���Ǵ���ԭ���ַ�����assetΪnil������ʧ��


## ����

### future = res.load(assetinfo, callback)

* load�ɹ������asset����assetinfo.cache.loaded�У��������Ҫ�ˣ���Ҫ����res.free��ע��Ҫ if err == nil �жϳɹ�����free����Ȼ�Ļ�����free�������ط���load��

* future �Ǹ�LoadFuture���󣬿ɵ���future:cancel()���������callback��û�����ã��������ٱ����á�


### future = res.wwwloader.load(url, callback)

* callback ����Ϊ (www)

## �ͷ�

### res.free(assetinfo)

1. ��������Դ��������load������assetinfo.cache.loaded�У�cache��refcnt�ģ���

2. ���û������load�˵��յ�����free������assetinfo.cache.cached�еȴ�lru��

3. �����ٵȴ�һ��ʱ�䣬���ܻᱻlru��ȥ��cache�в��ٳ��С�

## TODO

* wwwloader��priority֧�֣���ʱ��������Ҫʱд��

* assetbundle variant֧�֣�
