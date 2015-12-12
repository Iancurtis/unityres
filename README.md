# unityres
resource manager for unity slua 

## ��ʼ��

### res.init(editormode, abpath2assetinfo)

* editormode �������true����ʹ��ͬ������AssetDatabase.LoadAssetAtPath 

* abpath2assetinfo ��assetinfo.csvֱ�����ɡ����������������assetbundleʱ����cache������assetbundle��

### res.load_manifest(assetinfo, callback)

* assetinfo ��ʽΪ { assetpath: xx, abpath: xx, type: xx, location: xx, cache: xx }��Ӧ���Ǵ�assetinfo.csv�ж�ȡ����assetinfo.csv�ɴ���������ɡ�

* ����type ����Ϊ { assetbundle = 1, asset = 2, prefab = 3 }�� location ����Ϊ { www = 1, resources = 2 }��

* ����cache ΪCache���һ��instance������ʵ����lru��

* Լ������assetinfo��assetpath��Ϊnil����assetinfo.csv��assetpath��Ϊprimary key����typeΪasetbundleʱassetpath==abpath

* callback ����Ϊ (err, asset) errΪnilʱ����ɹ���


## ����

### future = res.load(assetinfo, callback)

* ����һ��future���󣬿ɵ���future.cancel()�������ͱ�֤����ص����ᱻ���á�

## �ͷ�

### res.free(assetinfo)

1. ��������Դ��������load������assetinfo.cache.loaded�У�

2. ���û������load�˵��յ�����free������assetinfo.cache.cached�еȴ�lru��

3. �����ٵȴ�һ��ʱ�䣬���ܻᱻlru��ȥ��cache�в��ٳ��С�


## res.wwwloader

### res.wwwloader.thread 

* ʵ���˶�WWW����Դ���ޡ�

* Ĭ��Ϊ5�� Ҳ����˵������5��WWW����Ȼ�������res.init��֮����Ĵ�ֵ

### future = res.wwwloader.load(path, callback)

* path ΪWWW�Ĳ���url

* callback ����Ϊ(err, www)

* ����future, �ɵ���future.cancel()�������ͱ�֤����ص����ᱻ���á�
