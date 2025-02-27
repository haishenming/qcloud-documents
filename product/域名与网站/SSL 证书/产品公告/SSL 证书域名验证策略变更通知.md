
根据 CA/Browser Forum 规定，自**2021年12月01日**起域名验证策略将会有以下重大变更：

**自2021年12月01日起，使用文件验证的域名，只能为当前被验证的域名签发 SSL 证书，不支持签发通配符 SSL 证书和其下级子域名 SSL 证书。**

目前，腾讯云 SSL 证书允许对主域名（例如 `dnspod.cn`）进行域名验证即可，适用于通配符证书（例如 `*.dnspod.cn` 或 `*.sub.dnspod.cn` 等）和其下级所有子域名（例如 `sub.dnspod.cn` 或 `sub2.sub1.dnspod.cn` 等）。

但从2021年12月01日起，对于使用文件验证方式的域名，只能为当前被验证的域名签发证书。例如，使用文件验证方式验证域名 `dnspod.cn`，则只能为 `dnspod.cn` 域名签发证书，不能为域名 `*.dnspod.cn` 或 `sub.dnspod.cn` 签发证书。

>! 因以上规定，腾讯云将于2021年11月21日停止泛域名证书的文件验证方式，敬请知悉。
