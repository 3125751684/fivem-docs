---
title: ����������
weight: 330
description: >
  �ڷ���������̨�����е������б�.
---

<!-- TODO: format this like client commands? -->

����ʹ��RCon����ֱ�Ӵӷ���������̨GUI�����������ã�ִ�п���̨�����ļ������ߣ����ACE������Դ��[ExecuteCommand]({{<native "EXECUTE_COMMAND">}})������

����Զ���RCon�������ͨ��ʹ�� [RegisterCommand]({{<native "REGISTER_COMMAND">}})��������ɡ�
���������򣨾ɰ棩`rconCommand`�¼���

### `start [resourceName]`

����������ָ������Դ�������ֹͣ����

����:

    start lambda-menu

### `stop [resourceName]`

ֹͣ������ָ������Դ���������������

����:

    stop mymode

### `ensure [resourceName]`

��������������ָ������Դ��������������� ������ǣ�������������ָ������Դ��

����:

    ensure my-testing-resource

### `restart [resourceName]`

��������������ָ������Դ���������������

����:

    restart lambda-menu

### `refresh`

����ɨ��*resources*�ļ��в��������е�����\_\_resource.lua�ļ���ʹ����Դ������ʹ�� [start](#start "wikilink")��ʼ��

����:

    refresh


### `status`

{{% alert theme="info" %}}������ **rconlog** �ṩ����Դ. {{% /alert %}}

��ʾ��������Ҫ��ʶ����������ID�����ƣ��˵��ping�Ĳ������б�

����:

    status

### `sv_maxClients [newValue]`

һ������̨��������ָ��������ͨ������ӵ�е����ͻ�������Ϊ1��64֮���������

### `sv_endpointPrivacy [newValue]`

һ�����������Ϊtrue����ӷ����������Log�������IP��ַ��

### `sv_hostname [newValue]`

�������������������ַ���������

### `sv_authMaxVariance [newValue]`

**Variance** �����ṩ�ߵ��û�ID���ĵĿ������Ƕ��� (i.e. 'steam', 'ip', or 'ros').

����̨������Ϊ1-5��������Ĭ��ֵ1���� ����С�����п��ܸı䡣

### `sv_authMinTrust [newValue]`

**Trust** ���Ƕ���ͻ�����ƭ�û���ݵķ�ʽ����̫���ܣ���

����̨������Ϊ1-5��������Ĭ��Ϊ5���� ����͵����������5���ⲿ���������֤֮��ķ�������

### `clientkick [id] [reason]`

{{% alert theme="info" %}}������ **rconlog** �ṩ����Դ. {{% /alert %}}

��������ԭ�򣬴ӷ�������ָ���ķ�����ID�� [status](#status "wikilink"))�ͻ��ˡ�

����:

    clientkick 43 You're a superstitious idiot!

### `say [message]`

{{% alert theme="info" %}}������ **chat** �ṩ����Դ. {{% /alert %}}

�����������ԡ�����̨����ʽ������Ϣ��

����:

    say Hi, everybody!


### `load_server_icon [fileName.png]`

����ָ����ͼ�겢��������Ϊ������ͼ�ꡣ ��ͼ�������96x96 PNG�ļ���

����:

```toml
load_server_icon "my-server.png"
```

### `add_ace [principal] [object] [allow|deny]`

�����ʿ�����Ŀ��ӵ��������ķ��ʿ����б��С�

����:

```
add_ace group.admin command.potato allow
add_ace identifier.steam:110000112345678 command.apple deny
```

### `add_principal [child_principal] [parent_principal]`

����һ��Ҫ����һ������̳е����塣

����:
```toml
# makes identifier.steam:110000112345678 inherit from group.admin
add_principal identifier.steam:110000112345678 group.admin
```

### `remove_ace [principal] [object] [allow|deny]`

�ӷ������ķ��ʿ����б���ɾ��ָ����ACE��

����:

```
remove_ace identifier.steam:110000112345678 command.apple deny
```

### `remove_principal [child_principal] [parent_principal]`

ɾ��ָ��������̳��

����:
```
remove_principal identifier.steam:110000112345678 group.admin
```

### `test_ace [principal] [object]`
�����Ƿ�����ί���˷��ʸ�������

����: `test_ace group.admin command.adminstuff`
