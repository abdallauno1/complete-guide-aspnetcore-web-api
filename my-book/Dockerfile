#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["my-book/my-book.csproj", "my-book/"]
RUN dotnet restore "my-book/my-book.csproj"
COPY . .
WORKDIR "/src/my-book"
RUN dotnet build "my-book.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "my-book.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "my-book.dll"]