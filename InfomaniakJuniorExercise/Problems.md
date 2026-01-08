
Sail permission denied
https://stackoverflow.com/questions/73476633/laravel-sail-up-throws-permissions-denied-error

Do a Http:get('http://localhost:3000/api/movies'); from sail container don't work.
-> use the container name in docker compose like http://movie-api:3000/api/movies