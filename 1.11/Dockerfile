# Bukkit for Docker
#     Copyright (C) 2015 Bren Briggs

#     This program is free software; you can redistribute it and/or modify
#     it under the terms of the GNU General Public License as published by
#     the Free Software Foundation; either version 2 of the License, or
#     (at your option) any later version.

#     This program is distributed in the hope that it will be useful,
#     but WITHOUT ANY WARRANTY; without even the implied warranty of
#     MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#     GNU General Public License for more details.

#     You should have received a copy of the GNU General Public License along
#     with this program; if not, write to the Free Software Foundation, Inc.,
#     51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

FROM openjdk:8-alpine as builder
WORKDIR /minecraft
RUN apk update
RUN apk --no-cache add wget git bash
RUN wget -O /minecraft/BuildTools.jar https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar
RUN java -jar BuildTools.jar --rev 1.11  2>&1 /dev/null

FROM openjdk:8-alpine
WORKDIR /root
RUN apk update
RUN apk --no-cache add bash
COPY --from=builder /minecraft/craftbukkit-*.jar /root
COPY --from=builder /minecraft/spigot-*.jar /root
EXPOSE 25565
WORKDIR /data
ADD entrypoint.sh /root/entrypoint.sh
ENTRYPOINT ["/root/entrypoint.sh"]
CMD ["craftbukkit"]
