---
title: ��CitizenMP.ServerǨ��
weight: 360
description: >
  ��һЩ���ϵķ���ˣ� �����й�Ǩ���Ϸ���˵�ָ�ϡ�
---

### Loading Scripts

`require`���ٴ��ڣ��κνű�/�ⶼӦʹ����Դ�嵥�е�`server_script`ָ����ء�

����:

``` lua
server_script "my_script.lua" -- load script
server_script "my_lib.net.dll" -- load a particular assembly into the .net appdomain
server_script "@resource_name/script.lua" -- load a script from another resource
```

Ҫ������ʱ�����ļ�������ʹ�� [LOAD\_RESOURCE\_FILE]({{<native "LOAD_RESOURCE_FILE">}}) (`LoadResourceFile("resource_name", "file_name")`), �������һ��Lua�ļ��������ʹ�á�

``` lua
load(...)
```

����Lua���룬������ʾ����ʾ��

``` lua
function loadLuaFile(resource, file)
    return load(LoadResourceFile(resource, file), file)()
end
```

### String Splitting

`str:Split` ���ٴ��ڣ���Ӧ��Ϊ��ʹ���ʵ���Lua������ ����ͨ������ճ���� `stringsplit` ���������ǣ�

``` lua
function stringsplit(inputstr, sep)
    if sep == nil then
        sep = "%s"
    end
    local t={} ; i=1
    for str in string.gmatch(inputstr, "([^"..sep.."]+)") do
        t[i] = str
        i = i + 1
    end
    return t
end
```

### Bitwise Operations

Lua 5.3������`bit32`����CfxLua����ʱδ�������� �����������������һ������λ��������Ҳ����ʹ����ͨ�������`��`��`|`��...����������

### CLR

NeoLua����ʹ�ã����`clr`�����ռ䲻�ٴ��ڡ� �����Ҫ����C \�����룬��ʹ��������.NET����ʱ�ͷ�����������

### TempIDs

�������ִ�С� playerConnecting���ڼ�������κ��ض��İ�λ���㣬����衰 source��ֵ����0x10000����ô�ڡ� playerConnecting���ڼ�ʹ�ú����Ͳ�����Ҫ�ˡ�
